---
tags:
  - daybreak
  - venture-capital
type:
author:
description:
aliases:
date created: Thursday, November 19th 2026, 12:15:13 am
date modified: Thursday, November 19th 2026, 12:15:18 am
---
A system that keeps a list of people and companies the fund should talk to before anyone else does, and sends them to partners weekly.

3 modules:
- **Detect.** Find signals from people that have started or are about to start company.
- **Predict.** Rank these people on how likely they are to found said company.
- **Deliver.** Summarize in a weekly email.

### Inputs

| Input                                                                                | How we handle it                                                                                                                                                           | Module  | Priority         |
| ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ---------------- |
| LinkedIn. Difficult but very good.                                                   | Licensed data vendor (Crustdata, Coresignal or People Data Labs). No in-house scraping.                                                                                    | M3      | High             |
| X: "good but low signal"; track people and their followers                           | Follow-graph diffs on a curated list (partners, top angels, scouts). Alert when ≥ N of them follow the same new account.                                                   | M4      | Medium           |
| "Partner followed a company"                                                         | A specific case of the above. It is the highest-precision X signal, so build it first.                                                                                     | M4      | High (within M4) |
| YC updates on LinkedIn ("table stakes")                                              | YC directory and Launch YC scraper, plus LinkedIn job-change detection for YC founders. Do the same for other accelerators (a16z speedrun, SPC, Neo, etc.).                | M2      | High (cheap)     |
| Discord and student groups                                                           | Semi-manual. Join the communities, use a bot only where admins allow it, track membership lists of student clubs and hackathons.                                           | M6      | Low/Medium       |
| **Labs, private groups and talent per university** (most interesting to the partner) | University Talent Map: universities → labs → PIs → students and postdocs, using OpenAlex, lab pages, GitHub, Devpost and student org pages. Seeded from "my college list". | M2 + M5 | **Highest**      |
| "Who is likely to start a startup" (Retterath)                                       | Founder-propensity score built from profile features. Starts as rules, becomes a model once we have labels.                                                                | M7      | High             |
| New vendors: Happenstance, Exa, RunaCap                                              | Time-boxed vendor evaluation (see §6).                                                                                                                                     | M8      | Parallel track   |
| Keep track of thoughts, Ramp card                                                    | `DECISIONS.md` log in this repo. All vendor spend on one Ramp card with a monthly budget. A `costs` table in the DB.                                                       | M0      | Day 1            |
| Infrastructure from zero                                                             | §3 and §4                                                                                                                                                                  | M0      | Day 1            |

---

## 3. Architecture

```
                ┌──────────────────────── Sources ────────────────────────┐
                │ LinkedIn vendor │ X API │ GitHub │ OpenAlex/arXiv │ YC   │
                │ HN/ProductHunt  │ Devpost │ Univ/lab pages │ Exa │ Discord│
                └────────┬───────────────────────────────────────────────┘
                         │ scheduled connectors (one per source)
                         ▼
   ┌──────────────────────────────────────────────────────────────────────┐
   │ RAW LAYER (Postgres jsonb + object storage for big payloads)         │
   │ raw_events(source, external_id, fetched_at, payload, cost_usd)       │
   └────────┬─────────────────────────────────────────────────────────────┘
            │ normalize + entity resolution
            ▼
   ┌──────────────────────────────────────────────────────────────────────┐
   │ CORE GRAPH (Postgres)                                                │
   │ person ─ affiliation ─ org (company / lab / university / club)       │
   │ person ─ identity (linkedin, x, github, email, orcid, …)             │
   │ signal(person|org, type, strength, evidence_url, observed_at)        │
   │ embeddings (pgvector) for fuzzy matching + semantic search           │
   └────────┬─────────────────────────────────────────────────────────────┘
            │ scoring jobs (rules → ML) + LLM summarization
            ▼
   ┌──────────────────────────────────────────────────────────────────────┐
   │ SCORES & LISTS: founder_propensity, momentum, thesis_fit, "why now"   │
   └────────┬─────────────────────────────────────────────────────────────┘
            ▼
   Slack digest (daily/weekly) ── Review UI (approve / pass / snooze) ── CRM push
            │                                   │
            └──────── partner feedback ──────────┘──► labels for M7 model
```

### Stack (recommended)

| Layer | Choice | Why |
|---|---|---|
| Language | Python 3.12, `uv` | Best data and ML ecosystem; vendor SDKs are in Python |
| DB | **Postgres on Supabase or Neon**, with `pgvector` | One store for relational data, JSON and vectors. Managed backups. Cheap. |
| Object storage | S3 / R2 | Raw HTML and large API payloads |
| Orchestration | **Start:** GitHub Actions cron or Modal scheduled functions. **Later:** Dagster or Prefect once there are more than about 15 jobs with dependencies. | Zero infrastructure to begin with |
| Scraping (only where allowed) | `httpx` + `selectolax`; Playwright for JS-heavy university pages; Apify for one-off actors | |
| LLMs | Claude Haiku for bulk extraction and classification; Claude Sonnet for "why now" summaries and lab-page parsing; batch API + prompt caching | Quality-to-cost ratio; batch API halves the price |
| Entity resolution | Deterministic keys first (LinkedIn URL, GitHub handle, ORCID, email), then name + affiliation + embedding similarity, with an LLM tie-breaker | |
| Delivery | Slack bot (digest + buttons) → Retool or a simple Next.js internal app later | Partners already live in Slack |
| CRM | Push to whatever the fund uses (Affinity, Attio or Notion). If nothing yet, **Attio** has a good API. | |
| Secrets / auth | Doppler or 1Password; Google SSO for the review UI | |
| Observability | Sentry + a `job_runs` table + a Slack alert when a job fails or returns 0 rows | Silent connector breakage is the main failure mode |

### Core schema (v1)

```
person(id, full_name, headline, location, first_seen, last_updated)
identity(person_id, kind, value, verified)          -- linkedin|x|github|email|orcid|scholar|discord
org(id, kind, name, domain, parent_org_id)         -- company|lab|university|club|accelerator|fund
affiliation(person_id, org_id, role, start, end, source)
signal(id, subject_type, subject_id, type, strength, evidence_url, observed_at, source, raw_event_id)
score(subject_id, model, value, features jsonb, computed_at)
watchlist(id, name, owner)  /  watchlist_member(...)
feedback(subject_id, partner, verdict, note, created_at)   -- labels
raw_event(...) / job_run(...) / cost_ledger(date, vendor, units, usd, job)
```

---

## 4. Modules and build order

Each phase ends with something partners can use. Estimates assume **one engineer full-time** plus AI coding tools.

### Phase 0: Foundations (weeks 1–2)

**M0 · Platform skeleton**
- Repo, `uv`, lint and tests, CI, secrets, Postgres plus migrations (Alembic or sqitch).
- Core schema above, a `raw_event` landing table, a connector base class (fetch → land raw → normalize → emit signals), and `job_run` and `cost_ledger` tables.
- Entity resolution v0, deterministic keys only.
- Slack bot that posts a test digest.
- `DECISIONS.md` (thought log) and a Ramp card with a budget alert set.
- **Done when:** a dummy connector runs on cron, lands data, and posts to Slack. Failures alert.

### Phase 1: Cheap, high-value sources plus the talent map (weeks 3–6)

**M1 · Seed lists.** Ingest "my college list", the partners' X handles, the fund's portfolio founders, and target accelerators. These are the root of everything else.

**M2 · Free and public connectors**
| Connector | Signal | Cost |
|---|---|---|
| YC directory and Launch YC | New batch companies, founders, and later pivots/status | Free |
| Other accelerators (SPC, a16z speedrun, Neo, Z Fellows, etc.) | Same | Free |
| GitHub API | Repo star velocity, new orgs created by watched people, "trending in our university list" | Free (rate-limited) |
| OpenAlex (+ arXiv) | Papers by institution → authors → labs. Key input for the talent map. | Free |
| HN (Algolia API) / Product Hunt | Show HN and launch posts by watched people | Free |
| Devpost / MLH | Hackathon winners at target universities | Free (scrape) |
| RunaCap ROSS index | Fast-growing OSS startups (quarterly) | Free |

**M5 · University Talent Map v1** _(the partner's top interest)_
1. For each university on the college list, use OpenAlex to get CS/EE/bio/etc. departments, then the most active labs and PIs by recent output.
2. Crawl lab "people" pages and use an LLM to extract them into `person` + `affiliation(role=PhD|postdoc|undergrad RA)`.
3. Add student orgs (entrepreneurship clubs, AI clubs, hackathon teams, venture fellowships), founder programs (e.g. CMU Swartz Center, Stanford StartX, MIT delta v, Berkeley SkyDeck), and the startup-y courses' public project lists.
4. Output a per-university page listing labs ranked by spin-out potential (industry funding, applied output, GitHub activity, alumni founder rate) and the people in them.
- **Done when:** partners can open "CMU" and see the top 20 labs and about 200 people, refreshed monthly.

### Phase 2: Paid people data (weeks 6–10)

**M3 · LinkedIn coverage via vendor**
- Pick one vendor after a 2-week bake-off on 500 known people from our graph: **Crustdata** (VC-focused, has real-time "watchers" for job changes), **Coresignal**, or **People Data Labs**. (Proxycurl shut down in 2025; do not build on unofficial LinkedIn scrapers.)
- Enrich every person in the talent map and the watchlists.
- **Change detection** on a refresh cadence (weekly for the top tier, monthly for the long tail). Signals:
  - Title contains "Stealth", "Founder", "Building something new", or "Exploring"
  - Left FAANG or a top AI lab with no new job listed
  - Headline change, new company page created, co-founder clusters (2+ watched people join the same new org)
  - YC founder LinkedIn updates (table stakes)
- **Done when:** a weekly "stealth / just left" digest goes out, and a partner rates at least 30% of its items as worth a look.

**M4 · X follow-graph tracking**
- Watch list: partners, about 100–300 top seed investors and operators, and scouts.
- Diff their `following` lists daily or weekly. A signal fires when ≥ 1 partner or ≥ 3 tracked investors follow the same new account within 14 days.
- Classify new accounts with an LLM (person vs. company, stealth or not, which domain) and link them to the graph.
- Data source: the official X API (pricing changes often; check current tiers) or a third-party read API (twitterapi.io-style, much cheaper but against ToS risk). Decide in M8.
- **Done when:** "N notable investors just followed @X" alerts flow to Slack.

### Phase 3: Prediction and workflow (weeks 10–16)

**M6 · Community sources (Discord, student groups, private groups)**
- Mostly human-in-the-loop. Partners or scouts join the relevant servers and groups. A bot is added only where admins allow it. Track membership and roles in hackathon/builder servers and links shared in them.
- Add a manual "add person/lab" form, so partners' own intel enters the graph and is not lost in DMs.
- Expect low automation ROI. Keep scope small.

**M7 · Founder-propensity scoring (Retterath-style)**
- **v0 (rules):** a weighted score on known predictors from the literature and Retterath's work: elite technical education, prior startup or early-employee experience, tenure at a fast-growing company, seniority plateau, published or OSS leadership, prior founder in network, recent vesting cliff (about 4 years at a company), leaving a job without a new one, co-founder proximity.
- **v1 (model):** gradient-boosted classifier. **Positives:** people in our graph who founded a company in the last 3 years (vendor data shows the transition). **Negatives:** matched peers who didn't. Features are time-sliced to avoid leakage (only use what was known *before* they founded). Retrain monthly. Partner feedback is a second label stream.
- **Outputs:** `founder_propensity` (will they found?), `momentum` (is something happening now?), and `thesis_fit` (LLM against the fund's thesis doc). The digest ranks on a mix of all three.
- **"Why now" card:** Sonnet writes 3 bullets per person, citing signals with links. No unsourced claims.

**M9 · Review UI and CRM sync**
- Retool or a small Next.js app: queue, person and lab pages, approve / pass / snooze / "already know".
- Approved items push to the CRM. Every action is stored in `feedback`.

### Parallel track

**M8 · Vendor evaluation** (see §6). Run it in weeks 2–8 alongside the build, because results change M3 and M4.

### Order at a glance

```
wk  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16
M0  ████
M1     ██
M2        ██████
M5        ████████████              (talent map, refresh ongoing)
M8     ██████████████               (vendor bake-offs)
M3                 ██████████
M4                       ██████
M7 rules                    ████    → model ███████
M6                                ████
M9                                   ██████
```

The first partner-visible value comes in **week 3** (YC and accelerator digest). The talent map v1 comes around **week 6**, and LinkedIn change alerts around **week 9–10**.

---

## 5. Costs (estimates; verify current vendor pricing before signing)

### One-time build
| Item | Estimate |
|---|---|
| Engineering, 1 FTE × 4 months | Internal salary, or about $60–120k for a contractor |
| Vendor trials / POCs | $0–2k (most give trial credits) |

### Monthly run-rate

| Item | Lean (MVP, ~10k people tracked) | Scaled (~200k people, 10+ universities) |
|---|---|---|
| Postgres (Supabase/Neon Pro) | $25–75 | $200–600 |
| Compute / cron (GitHub Actions, Modal) | $0–50 | $100–400 |
| Object storage | <$10 | $20–50 |
| **LinkedIn data vendor** | $500–1,500 | $3,000–10,000+ (often annual contracts of $30k–100k+) |
| **X data** | $0–200 (third-party read API or basic tier) | $500–5,000 (official higher tiers are expensive) |
| Exa (search / websets) | $50–300 | $500–2,000 |
| Happenstance | ~$0–100 per seat (if adopted) | per-seat |
| LLM API (Claude, batch + caching) | $100–400 | $1,000–3,000 |
| Apify / proxies for allowed scraping | $0–50 | $100–300 |
| Retool / internal UI | $0–50 | $100–500 |
| Sentry, Doppler, misc. SaaS | $0–50 | $100–200 |
| **Total** | **≈ $1–3k / month** | **≈ $6–20k / month** |

**Benchmark:** off-the-shelf VC sourcing platforms (Harmonic, Specter, etc.) typically cost tens of thousands of dollars per year per fund. The build case only holds if the **university and lab talent map plus propensity scoring** are a real edge. Generic company tracking is not. Consider buying Harmonic or Specter for generic company coverage and building only the differentiated parts. That decision belongs in `DECISIONS.md` after M8.

**Cost controls:** one Ramp card for all sourcing vendors with a monthly cap. `cost_ledger` is reconciled monthly against Ramp. Tiered refresh: only the top ~5% of people get weekly enrichment. Use LLM batch API and caching. Never re-enrich a profile that hasn't changed (use the vendor's "last updated" field).

---

## 6. Vendor evaluation (M8)

Score each vendor on the same 500-person test set (known founders, stealth people and lab students).

| Vendor | What it is | Test |
|---|---|---|
| **Happenstance** | AI people search over your team's networks (LinkedIn, Gmail, etc.) | Coverage of warm paths to talent-map people, and quality of "find me ex-[lab] PhDs now in stealth" queries. Probably a **partner tool**, not a pipeline source, unless it has an API. |
| **Exa** | Neural web search API, plus people and company search and Websets | Discovery of lab pages, personal sites, stealth landing pages, and "people like X" queries. Strong candidate to power M5 crawling. |
| **RunaCap** | Runa Capital's ROSS index (fastest-growing OSS startups) and related public data | Free quarterly ingestion into M2. Low effort. |
| Crustdata / Coresignal / PDL | LinkedIn-derived people and company data | Freshness (days since change), match rate, job-change latency, price per record |
| Harmonic / Specter | Turnkey VC sourcing platforms | Overlap with what we would build; buy vs. build for company tracking |
| X API vs. third-party | Follow-graph data | Price per 1k follow lookups, ToS risk |

Evaluation metrics: **coverage** (% of the test set found), **freshness** (median lag of job changes), **precision** of signals, **$ per useful lead**, and **API ergonomics**.

---

## 7. Maintenance

| Area | Ongoing effort | Notes |
|---|---|---|
| Connector breakage (site and API changes) | 2–4 hrs/week | University pages and scrapers break most often. Alert on zero rows or schema drift. |
| Entity resolution fixes and dedup | 1–2 hrs/week | Merge/split tool in the review UI |
| Talent map refresh (new labs, students graduate) | Monthly job + ~4 hrs/month review | Academic-year cadence: big refresh in Sept and Jan |
| Scoring model retrain and eval | ~1 day/month | Track precision@20 of the digest against partner verdicts |
| Vendor and contract management, cost reconciliation | ~2 hrs/month | Ramp ↔ `cost_ledger` |
| Partner feedback triage / new asks | 2–4 hrs/week | |
| **Total steady state** | **≈ 0.3–0.5 FTE** | After the 4-month build, one engineer can run it part-time and keep extending it |

**Key risks**
- **Legal / ToS:** no direct LinkedIn scraping. Read the vendor data-licensing terms. Students and EU residents bring GDPR/FERPA considerations: store only public professional data, keep a deletion path, and do not ingest private Discord content without consent.
- **Signal noise:** X and Discord are low-signal. Gate them behind thresholds and keep them out of the main digest until precision is proven.
- **Adoption:** a digest nobody reads is worthless. Keep it to ≤ 10 items a day, each with a "why now", and measure open and action rates.
- **Vendor lock-in:** keep raw vendor payloads and our own IDs, so vendors can be swapped.

---

## 8. Success metrics

- **Leading:** partner action rate on the digest (target > 30%), precision@10, and freshness (time from signal to Slack < 48h).
- **Lagging:** number of first meetings sourced by the engine per quarter, % of new deals where we were early (first contact before their announced round), and term sheets attributable to the engine.

---

## 9. Open questions for the partner

1. Which universities are on "my college list", and how many? This drives talent-map scope and cost.
2. Thesis areas, for `thesis_fit` (AI infra, bio, deep tech…)?
3. Current CRM, if any?
4. Budget ceiling per month, and appetite to buy Harmonic or Specter for generic coverage?
5. Which partners' X and LinkedIn networks can we use (follow graphs, Happenstance connections)?
6. Who reviews the digest daily, and how quickly do they need alerts?

---

## 10. Immediate next steps (this week)

- [ ] Get answers to §9 questions 1, 3 and 4
- [ ] Create a Ramp card for sourcing tools with a budget alert
- [ ] Start `DECISIONS.md`
- [ ] Request trials: Exa, Happenstance, Crustdata, and one of Coresignal/PDL
- [ ] Scaffold the repo (M0) and stand up Postgres + Slack bot
- [ ] Build the YC + accelerator connector as the first live digest