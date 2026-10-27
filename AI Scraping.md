- One of the most hyped infastructure category currently.
- Demand is being driven by AI labs that need training and grounding data, and by the wave of AI agents that need to read and act on live web pages.
- Exa, Firecrawl, Oxylabs, Browserbase and others raised large rounds in the last 18 months.
- $1.6 billion market with 17% CAGR
- Largest incumbents have $300 million ARR

##### The horizontal layer is taken

Generic “turn any website into clean data for LLMs” APIs (Firecrawl, Exa, Tavily, Apify, Bright Data, Oxylabs, Zyte) are crowded, well funded, and racing to the bottom on price.

##### Value moving up the stack
Buyers want the finished, monitored dataset or the workflow outcome (price alerts, tender leads, compliance checks), not raw pages. Bright Data now sells e-commerce intelligence starting around $2,000 per month per product line.

##### US law is favorable to public data scraping

Courts have sided with scrapers on public data (Meta and X v. Bright Data; Google v. SerpApi dismissed; Amazon v. Perplexity injunction vacated).

In Europe, GDPR applies **even if it’s public data**.

##### Access is getting harder

Cloudflare blocks AI crawlers by default on new domains. Roughly half of top sites already do it. Cloudflare also has a pay-per-crawl product.

# What is scraping and what does AI have to do with it

- Classic scraping was a script hand-written code per website that broke whenever the site changed (show example).
- Agents can:
	- Read a page and **extract structured fields without site-specific code**
	- Repair or regenerate extractors when layouts change
	- (Sort of) drive a browser like a user

| Layer                   | What it does                                                    | Representative players                                  |
| ----------------------- | --------------------------------------------------------------- | ------------------------------------------------------- |
| Unblocking              | Residential/mobile IPs, CAPTCHA and anti-bot handling           | Bright Data, Oxylabs, Zyte                              |
| Browsers                | Hosted headless Chrome for agents and scrapers                  | Browserbase, Browserless, Browser Use                   |
| Crawl and extract APIs  | URL in, clean Markdown or JSON out; site-wide crawls            | Firecrawl, Apify, ScrapingBee, Zyte API                 |
| AI search APIs          | Query in, ranked and summarized web results out                 | Exa, Tavily, SerpApi                                    |
| Ready-made datasets     | Pre-collected, refreshed data on popular sites                  | Bright Data datasets, Oxylabs datasets                  |
| No-code / agentic tools | Point-and-click or natural-language scraping for non-developers | Browse AI, Bardeen, Nimble, Browserbase Director        |
| Vertical data products  | Domain-specific datasets, monitoring and alerts                 | Fornova (hotel pricing), price-intel and lead-gen tools |

The lower layers are capital-intensive and commoditizing; the upper layers depend on domain knowledge and distribution.

# Competitive landscape

The field splits into profitable incumbents that grew up on proxies, and venture-backed AI-native companies built around LLM-ready output and agents.

|Company|Positioning|Scale / funding (latest public)|
|---|---|---|
|Bright Data|Proxies, scrapers, datasets, MCP server for agents; the incumbent leader|>$300M ARR in 2025, 50%+ growth, guiding to $400M by mid-2026; PE-owned (EMK)|
|Oxylabs|Proxies, scraper APIs, AI parsing, datasets; bought ScrapingBee (2025)|~$350M ARR; $130M from Warburg Pincus (Jul 2026) at a reported $3.6B group valuation|
|Firecrawl|Developer API turning sites into LLM-ready data; open source|$75M Series B (Sep 2026); 1.5M+ users, 150K companies, ~40K in Brazil; ~180K GitHub stars|
|Exa|AI-native search engine and web retrieval API|$250M Series C at $2.2B (May 2026, a16z); 5,000+ companies|
|Tavily|Search API for LLM/RAG workflows|Acquired by Nebius, Feb 2026, reported $275M (some reports up to $400M)|
|Apify|Scraping platform plus marketplace of 75K+ “Actors” built by developers|~$40M ARR end-2025 (from $15M), 25K customers, profitable, minimal VC|
|Browserbase|Cloud headless browsers for agents; Stagehand SDK; Director no-code|$40M Series B at $300M (Jun 2025); $67.5M total|
|Zyte|Managed scraping and Zyte API; long-standing (ex-Scrapinghub)|Top performer in a late-2025 third-party unblocking benchmark|
|Browse AI, Bardeen, Nimble|No-code and agentic scraping for business users and sales teams|Seed to growth stage|

# Technology trends

|Trend|What it means|Implication for a startup|
|---|---|---|
|LLM extraction|Models read a page and return structured fields to a schema, no per-site selectors|Lowers build cost; anyone can do it, so it is not a moat by itself|
|Self-healing scrapers|LLMs generate selectors, detect breakage and regenerate (e.g., Oxylabs’ parser generates XPath and validates with Pydantic, caching selectors)|Big cost lever: use LLMs to build and repair cheap deterministic extractors, not on every page|
|Agentic browsing|Agents click, scroll and fill forms in cloud browsers|Unlocks data behind interaction; slower and costlier per page|
|Data validation|AI used to detect anomalies and enforce schemas on extracted data|Quality and freshness guarantees become the product|
|Agent protocols|MCP servers (Bright Data, Browserbase, Apify) and machine payments (Apify supports x402)|Distribution through agent ecosystems; paid access may become programmatic|
|Code generation for crawlers|AI writes spiders and scraping code end to end|Shrinks the advantage of large scraping engineering teams|

Since July 2025 Cloudflare has blocked known AI crawlers by default for new customers and launched **Pay Per Crawl**, which answers crawlers with HTTP 402 (Payment Required) and a price, with Cloudflare acting as merchant of record. From September 15, 2026, new Cloudflare domains get defaults that block training and agent crawlers on pages showing ads, while search crawlers remain allowed. Cloudflare sits in front of roughly 20% of the web, more than a million customer sites had already turned on AI blocking before the default changed, and studies cited in the press found 48% of top global sites blocking AI crawlers.

- **Costs rise:** more residential proxies, more browser rendering, more failed requests.
- **Legal exposure rises:** evading an active anti-bot system is exactly the conduct the newest lawsuits target (see section 7).
- **A new market opens:** permissioned, paid access. Firecrawl has said it wants licensed partnerships so content owners get paid when their content powers AI. Tooling for compliant, metered access is an opportunity, not only a threat.

|Case|Status|What it signals|
|---|---|---|
|hiQ v. LinkedIn|Foundational (2019–2022)|Scraping public data is not “unauthorized access” under the CFAA; later breach-of-contract findings went against hiQ|
|Meta v. Bright Data|Meta lost a key ruling and dropped the case (2024)|Site terms didn’t bind logged-off scraping of public data|
|X Corp v. Bright Data|Dismissed (2024)|Win for scrapers, but the court said public-data scraping can still breach terms in some cases|
|Google v. SerpApi|Dismissed Jul 20, 2026|DMCA anti-circumvention claim failed because ordinary search results aren’t protected works; commentators note the ruling leaves room for other anti-bot claims|
|Reddit v. SerpApi, Oxylabs, AWMProxy, Perplexity (SDNY)|Motion to dismiss largely denied Jul 31, 2026|DMCA circumvention and conspiracy theories can reach both scraping vendors and their customers; Reddit had standing via lost licensing revenue|
|Amazon v. Perplexity (9th Cir.)|Injunction vacated Aug 4, 2026; Amazon sought en banc rehearing|An AI agent acting on a user’s instruction may not itself “access” the site under the CFAA; ToS claims continue|

The live risk has shifted to **DMCA §1201 anti-circumvention** (defeating technical access controls), **contract/terms claims** (especially if you ever log in or accept terms), and **copyright** on how the output is used. Vendors can be sued alongside customers.

# Business models and unit economics

|Model|Examples|Notes|
|---|---|---|
|Usage / credits API|Firecrawl, Tavily (credits), Bright Data (four different meters)|Easy to adopt; price competition is intense; revenue is volatile with customer usage|
|Infrastructure by the hour/GB|Browserbase: plans from $20 and $99/month; extra browser time ~$0.10–0.12/hr; proxy ~$10–12/GB|Margins set by cloud compute and proxy bandwidth|
|Dataset subscriptions|Bright Data datasets and Insights (e-commerce intelligence from ~$2,000/month per product line)|Higher value per customer; collection cost is shared across customers|
|Marketplace|Apify Store: paid ~$1.6M/month to tool creators by Sep 2026|Network effects; platform takes a revenue share|
|Managed service|Zyte, PromptCloud-style done-for-you data feeds|Sticky enterprise contracts; services-heavy margins|
|Vertical SaaS on web data|Price intelligence, tender/lead monitoring, compliance monitoring|Sells outcomes; buyer is a business team, not a developer|
## Cost structure to model

- **Proxies and bandwidth**: usually the largest variable cost on protected sites.
- **Browser rendering**: needed for JavaScript-heavy pages and agentic flows; far costlier than plain HTTP.
- **LLM tokens**: manageable if models build and repair extractors rather than run on every page.
- **Maintenance**: sites change constantly. Self-healing extraction is what keeps this from scaling with headcount.
- **Legal and compliance**: counsel, DPIAs and legitimate-interest assessments in the EU, takedown handling.

**Why vertical beats horizontal on economics**

A horizontal API sells each page once, at a commodity price. A vertical data product collects a page once and sells the resulting dataset to many customers, at a price tied to the business value of the decision it informs. Bright Data’s own move into $2,000+/month insight products is evidence of where margin lives.

# Opportunity map

Ratings are qualitative judgments from the research above. “Fit” refers to the founder profile described in section 10.

|Opportunity|Competition|Legal risk|Defensibility|Fit|
|---|---|---|---|---|
|Generic scrape/crawl API for LLMs|Very high|Medium|Low|Low|
|Proxy / unblocking network|Very high|High|Medium (capital)|Low|
|Vertical data product: legal and public records (court dockets, gazettes, regulatory filings)|Medium|Low–medium|High|High|
|Vertical data product: public procurement and tenders (Brazil/LatAm)|Low–medium|Low|High|High|
|Vertical data product: e-commerce / marketplace price intelligence (LatAm)|Medium–high|Medium|Medium|Medium|
|Self-healing extraction for companies running fragile in-house scrapers|Medium|Low|Medium|High|
|Compliance and provenance layer (licensing, pay-per-crawl integration, audit trails)|Low–medium|Low|Medium–high|Medium|
|Enterprise “bring your own web data” agents for internal workflows|Medium|Medium|Medium|High|
# 3. Review of Six Medical Data Platforms

## 3.1 Overview

| Platform | Core asset | Accessible for scraping? |
|---|---|---|
| UWorld | Board-prep question bank with answer-level performance data from millions of students | No: paywalled, copyrighted, performance data is internal |
| AMBOSS | Integrated knowledge library and question bank, plus learner and clinician search data | No: login-gated, search data is internal |
| Figure 1 | Crowdsourced clinical images with physician comments and diagnostic discussion | No: login-gated, patient image consent and privacy risk |
| Radiopaedia | Tens of thousands of curated radiology cases with annotated imaging and diagnoses | Publicly viewable but licensed CC BY-NC-SA (no commercial use); commercial licensing is available |
| VisualDx | Diagnostic image library (strong in dermatology) tagged with clinical metadata | No: paid product, licensed images |
| Sermo | Physician-only forum with case discussions and large-scale physician polling | No: restricted to verified physicians, polling data is their commercial product |

## 3.2 Platform notes

**UWorld.** The most valuable asset isn't the questions, which are copyrighted, but the performance data: which distractors mislead which learners, and how often. That data never appears publicly.

**AMBOSS.** Besides its curated content, AMBOSS has behavioral data on what clinicians and learners search for. That's a signal of real-world information needs, and it's entirely internal.

**Figure 1.** Clinical images are high-risk even when de-identified. Consent was given for use on the platform, not for redistribution or training third-party models.

**Radiopaedia.** The most "open" platform on the list, but its non-commercial license rules out direct commercial reuse. It has licensed data commercially before, so a partnership is a realistic route.

**VisualDx.** A commercial product built on licensed images and expert tagging. The tagging and clinical metadata are the value, and they're proprietary.

**Sermo.** Its physician polling and discussion data is sold to pharma and research firms. Scraping it would mean taking the company's core revenue product.

## 3.3 Risks of scraping these platforms

- **Contractual:** violating terms of service, particularly for login-gated content.
- **Copyright:** commercial use of copyrighted questions, text and images.
- **Licensing:** violating the non-commercial terms of Creative Commons content.
- **Privacy and consent:** redistributing clinical images and patient-related content outside the consent under which they were shared.
- **Business:** healthcare buyers and investors run data-provenance diligence. Data obtained improperly can block sales, fundraising and acquisition.

# 4. The Core Lesson: Product-Generated Data Moats

Each platform's defensibility comes from data its own users generate:

| Platform | Content that attracts users | Proprietary data users generate |
|---|---|---|
| UWorld | Questions and explanations | Answer-level performance |
| AMBOSS | Knowledge library | Search and query behavior |
| Figure 1 | Case feed | Contributed images and discussion |
| Radiopaedia | Case library | Contributed and curated cases |
| VisualDx | Diagnostic tools | Clinical usage and expert tagging |
| Sermo | Physician community | Polls and case discussion |

Content brings users in, and users produce data no competitor can copy. A new company should aim for the same loop and not try to copy the content.

# 5. Viable Strategic Paths

## 5.1 License or partner

Some of these platforms (for example Radiopaedia, VisualDx and Sermo) already license or sell data. A startup can add value on top through structuring, benchmarking or building AI evaluation sets, under a licensing or revenue-share agreement. The partnership itself becomes a barrier to entry.

## 5.2 Build on open data, then generate proprietary data

Start with openly licensed sources to launch a product, then capture usage data from it. Sources with friendlier licensing:

- **PubMed Central Open Access, commercial-use subset:** case reports with images.
- **MedPix (National Library of Medicine):** medical images and teaching cases.
- **ISIC Archive:** dermatology images (licenses vary per image).
- **The Cancer Imaging Archive (TCIA):** imaging collections (licenses vary per collection).
- **openFDA:** drug labels, adverse events, device data.

Check the license for each dataset, and each subset, before commercial use.

Examples: a case-based learning tool, a diagnostic reasoning trainer, or a clinical AI evaluation workbench. In each, user interactions become the proprietary dataset over time.

## 5.3 Clinician-validated evaluation data for AI companies

Model developers and health-AI startups increasingly need clinically validated benchmarks and expert-graded responses. A possible pipeline:

1. Use LLMs to draft clinical cases and questions from openly licensed literature.
2. Have paid, credentialed clinicians review, correct and grade them.
3. Sell the validated evaluation sets, or run evaluations as a service.

The moat is the expert-validation pipeline and the accumulated grading data, which parallels UWorld's performance data. This path fits an "LLM + datasets" thesis best and avoids the legal risks above.