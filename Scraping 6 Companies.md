
| # | Platform | Data of interest | Access model |
|---|---|---|---|
| 1 | **UWorld** | Board-prep question bank; answer-level performance data from millions of students | Paid subscription |
| 2 | **AMBOSS** | Knowledge library and question bank; learner and clinician search data | Paid subscription (German company) |
| 3 | **Figure 1** | Crowdsourced clinical images with physician comments | App or account; patient images |
| 4 | **Radiopaedia** | Tens of thousands of annotated radiology cases | Largely public; CC BY-NC-SA; commercial licensing program |
| 5 | **VisualDx** | Diagnostic image library (dermatology-heavy) with clinical metadata | Paid subscription |
| 6 | **Sermo** | Physician-only forum; case discussions; polling data | Verified-physician login |

**Sending a request to each company’s homepage and robots.txt**

| Site        | Homepage HTTP status   | Bot blocking             | `robots.txt` highlights                                                   |
| ----------- | ---------------------- | ------------------------ | ------------------------------------------------------------------------- |
| UWorld      | 200 OK                 | None at the front door   | Disallows demo pages, question-bank pages, `/terms.asp`, `/subscribe.asp` |
| AMBOSS      | 302 redirect           | None at the front door   | Disallows `/api/`, `/search`, `/account/`, and `?format=json` variants    |
| Figure 1    | **403 Forbidden**      | Yes (Cloudflare-managed) | `Content-Signal: search=yes, ai-train=no`; blocks AI training crawlers    |
| Radiopaedia | **406 Not Acceptable** | Yes (Cloudflare-managed) | `Content-Signal: search=yes, ai-train=no`; blocks AI training crawlers    |
| VisualDx    | 200 OK                 | None at the front door   | Disallows `/articles/`, `/account/`, `/purchase/`                         |
| Sermo       | **403 Forbidden**      | Yes                      | Only disallows `/wp-admin/`; publishes a sitemap of its marketing pages   |
# Legal?

| Approach                                                                                | Risk               | Key authority                                                                                                                                                                                                                                       |
| --------------------------------------------------------------------------------------- | ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Scraping **public, logged-out pages** without getting around blocks                     | **Low**            | *hiQ Labs v. LinkedIn* (9th Cir. 2022): scraping publicly accessible data likely isn't "without authorization" under the CFAA. *Meta v. Bright Data* (N.D. Cal. 2024): terms of service didn't bind a logged-out scraper.                           |
| **Getting around bot blocks** (Cloudflare, IP bans, spoofed headers, headless browsers) | **Medium to high** | *Craigslist v. 3Taps* (N.D. Cal. 2013): continuing to scrape after an IP block and a cease-and-desist was unauthorized access under the CFAA. Deliberate evasion is evidence you knew you lacked permission.                                        |
| Scraping **from inside a paid or verified account**                                     | **High**           | Clear **breach of contract**, since the terms were accepted at signup (hiQ ultimately lost on this point in 2022). Possible CFAA exposure. Possible **DMCA §1201** anti-circumvention claims for getting past access controls on copyrighted works. |

### Companies that crossed the line

| Company          | What happened                                                                                                                              |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **Clearview AI** | Scraped facial images. Fined tens of millions across several EU countries; large US class-action settlement.                               |
| **Proxycurl**    | Shut down in 2025 after LinkedIn sued it over scraping through fake logged-in accounts.<br>**I used this to scrape LinkedIn back in 2023** |
| **hiQ Labs**     | Won the CFAA fight but lost on breach of contract; went out of business.                                                                   |
