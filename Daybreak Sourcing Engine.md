---
tags:
  - daybreak
  - venture-capital
type:
author:
description:
aliases:
date created: Thursday, November 19th 2026, 12:15:13 am
date modified: Thursday, November 19th 2026, 2:53:50 pm
---
[[Daybreak]]

Goal: 

> Build an automated engine that finds people and companies **before** they raise. That means people who just started something and people likely to start something soon. It sends them to partners with a short "why now".

## 1. Sources

### Ranking

| Rank | Source                                  | Cost          |
| ---- | --------------------------------------- | ------------- |
| 1    | University labs & talent                | Free          |
| 2    | LinkedIn                                | Low           |
| 3    | X (follow graph)                        | Low           |
| 4    | Student groups, hackathons, fellowships | Free          |
| 5    | GitHub                                  | Free          |
| 6    | YC & accelerators                       | Free          |
| 7    | Exa                                     | Low           |
| 8    | Happenstance                            | Free–low      |
| 10   | Discord & private communities           | Free (manual) |

### 1.1 University labs & talent

**Why.** This is where future founders sit 1–3 years before they found anything, and few funds map it systematically. Raw data is free, the work is in the structure.

**Why not / limits.** Lab pages are messy and go stale, students don’t announce anything there. This source tells us **who to watch**, and other sources tell us **when they move**.

**Signals** (suggestion)

- Lab has a history of spin-outs or alumni founders
- Applied output
- Student finishing their PhD
- GitHub activity

**How**

1. **Seed** from my college list
2. Crawl lab for people. This will probably be done by an LLM.
3. **OpenAlex API** for recent works. Rank by output but also industry co-authorship.
4. Crawl founder programs (e.g. CMU Swartz Center, Stanford StartX), venture competitions and their winners, startup courses with public project lists.
5. Score by both spin-out potential (lab-wide) and founder profile (individuals)
6. Refresh **monthly or bimonthly**

**Cost.** OpenAlex is free. Modal for crawlers at about $10 per month. LLM extraction costs about $5 per university

**Risks.** Parsers can break when lab sites change. We can counter that with browser-based LLM.

---

### 1.2 LinkedIn

**Why.** It has the most direct "I just started something" signals: titles like Stealth, Founder or "Building something new", leaving a job with no next job, and two watched people joining the same new company.

**Why not.** Hostile to automation. Proxycurl case. Enterprise data vendors (Crustdata, Coresignal) are good but cost $1k+ per month, which is outside our budget. Exclusivity is low because every fund watches LinkedIn.

**Signals**

- Title or company changes to "Stealth", "Founder", "Co-founder" or "Building"
- Left a top company or lab with no new role listed (sabbatical or "exploring")
- Four or more years at a company (vesting cliff passed) plus a headline change
- Two or more watched people join the same new or unknown org (co-founder cluster)
- YC/accelerator founders posting batch updates (table stakes)

**How (cheapest first)**

1. **Sales Navigator seat (about $100/month), worked by a human.** With list of leads.
2. **Pay-per-result profile fetches.** Use Apify LinkedIn profile actors that need no login (roughly $3–10 per 1k profiles).

**Cost.** About $100–150/month with Sales Navigator, or about $15–40/month with automation only.

**Risks.** Apify actors break or get blocked.

---

### 1.3 X

**Why.** "A partner followed a company" is the highest-precision signal on X. When several good seed investors follow the same new account within a short window, it usually means a stealth company or a founder about to raise.

**Why not.** The official X API is priced far above our budget. Third-party read APIs are cheap but violate X's terms of service.

**Signals**

- At least 3 tracked investors follow the same account within 14 days (weighted by how good each investor is)
- The new account is a company with few followers, a "stealth", "building" or "soon" bio, or a link to a landing page
- The new account belongs to someone already in our graph

**How**

1. Watchlist: about 100–300 hand-picked seed investors, scouts and top operators. 
2. Follow lists come back newest-first, so each week we fetch **only the first page** (about 200) of each account's following list and diff it against the last snapshot. 
3. Aggregate new follows across accounts in a sliding 14-day window and fire a signal when it crosses the threshold.
4. A Haiku call classifies each new account as person or company, decides whether it looks like stealth, assigns a domain, and links it to the graph by handle or name.
5. Cheapest data option: a third-party read API such as twitterapi.io (roughly $0.15 per 1k items; verify). 300 accounts × 200 items × 4 weeks ≈ 240k items ≈ **$35/month**. Weekly polling of 100 accounts costs about $10/month. The official X API is only worth it if pricing changes.

**Cost.** About $10–40/month.

**Risks.** Breaching X's terms through the third-party API, and the vendor disappearing.

---

### 1.4 Student groups, hackathons, fellowships

**Why.** Undergrads and master's students who run entrepreneurship clubs, win hackathons, or get into fellowships (Z Fellows, Neo Scholars, Thiel, Contrary, a16z speedrun applicants, and so on) are very likely to become founders, and they show up here years early. This complements the lab map, which covers PhDs and postdocs.

**Why not.** Data is spread across many small sites, and people in it are hard to match to records from other sources.

**Signals**

- Officer roles in entrepreneurship, AI or robotics clubs
- Hackathon wins, repeat wins especially (Devpost, MLH, TreeHacks, HackMIT, …)
- Fellowship or scholar announcements
- University venture competition finalists

**How**

1. Scrape Devpost hackathon galleries (winners, team members, GitHub links), filtered to universities on the college list.
2. Use Exa to find club officer pages, fellowship cohort announcements and pitch competition results. Haiku extracts the people.
3. Hand every person off to the GitHub, LinkedIn and X watchlists.

**Cost.** Free, apart from small LLM and Exa costs.

**Risks.** Matching names to other records is hard here. Require a second identifier (GitHub, school email domain or LinkedIn) before merging records.

---

### 1.5 GitHub

**Why not.** Most repos are noise, and most early work is private. We watch Runa Capital’s list instead.

---

### 1.6 YC & accelerators

**Why not.** Every fund sees it at the same time, so it gives us almost no edge.

What do you think?

---

### 1.7 Exa

**Why.** Exa is a semantic search API. It is the cheapest way to cover the long tail of the web: personal sites, lab pages, blog posts and new landing pages. It also powers discovery for previous stuff.

**Why not.** Signal precision is weak on its own, and costs grow with query volume.

**Signals**

- New landing pages that look like stealth companies
- Personal sites updated with "building X" or "leaving Y"
- Lab and club pages for the talent map

**How**

- Run a fixed set of saved queries weekly, with each URL deduplicated against what we've already seen.
- Use it on demand from the other connectors.
- Run "find similar" on companies partners liked.
- Skip Websets (its bulk product) until there is budget.

**Cost.** Pay-as-you-go, about $10–50/month at our volume, starting with free credits (verify pricing).

---

### 1.8 Happenstance: partners' networks

**Why not.** It is a tool for partners to search with, not a data feed. It is more useful in the outreach stage.

---

### 1.9 Product Hunt

**Why not.** Launches are late and public, so many funds see them.

---

### 1.10 Discord & private communities

**Why.** Builder communities (AI and robotics servers, hackathon servers, university Discords) are where students and hackers show off work early.

**Why not.** Automating it is mostly off-limits. Self-bots, meaning automated user accounts, break Discord's terms of service. Bots need an admin invitation, and private content needs consent. The signal-to-noise ratio is low.

**How**

- Partners or scouts join the relevant servers themselves and drop interesting people into the intake form.
- I will source interesting servers and communities to keep an eye.

---


## 2. Design

### 2.1 System diagram

![[Daybreak Sourcing Engine-1.png]]

### 2.2 Entity resolution

Entity resolution runs in three passes:

1. **Exact match** on a strong key: LinkedIn URL, GitHub handle, ORCID or email.
2. **Fuzzy match:** name, affiliation and embedding similarity using `pgvector`.

### 2.3 Scoring

See Data Driven VC’s research.
- We need a feedback loop as well: adjust weights based on reviews

### 2.4 Estimated running costs

| Item                                                   | Minimum           | Comfortable      |
| ------------------------------------------------------ | ----------------- | ---------------- |
| Postgres: Supabase free tier, then Pro                 | $0                | $25              |
| Compute: GitHub Actions free minutes, or a Hetzner VPS | $0                | $6               |
| Object storage: Cloudflare R2 free tier (10 GB)        | $0                | $0–5             |
| LinkedIn: Sales Navigator seat                         | $0 (skip)         | ~$100            |
| LinkedIn: Apify pay-per-result                         | $15               | $40              |
| X follow graph (third-party API)                       | $10               | $40              |
| Exa                                                    | $0 (free credits) | $50              |
| LLM (Claude Haiku, batch + caching; Sonnet sparingly)  | $20               | $80              |
| GitHub, OpenAlex, YC, HN, Devpost, ROSS                | $0                | $0               |
| Slack, Sentry, Retool free tiers                       | $0                | $0               |
| **Total**                                              | **≈ $45/month**   | **≈ $350/month** |

## 4. Schedule

Each step ends with something usable. Steps marked ⟂ can run in parallel with the ones next to them.

1. **Foundations:** repo, database, connector base class.
2. **Seed lists:** the “who to watch part”.
	- 
___

1. **University talent map:** OpenAlex, then lab pages, then people. Per-university pages for partners.
2. **Student groups & hackathons:** and the **manual intake form**. These extend the talent map to undergrads.
3. **GitHub.**
4. **LinkedIn:** needs more research before settling on an approach.
5. **X follow graph:** this is likely the most complicated code.
6. **Scoring and send**
7. Discord & communities watch list

---
