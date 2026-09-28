---
tags:
  - software
type: note
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Monday, September 28th 2026, 5:28:35 pm
date modified: Monday, September 28th 2026, 5:28:40 pm
---
Low-code platform from Microsoft.

- Looks a lot like Airtable + interfaces
- They have some AI-driven capabilities but it’s all Copilot
- Part of the overall ecosystem hence Entra ID integrates, role-based access

Four ways to build an app:
1. Canvas Apps: Drag-and-drop UI on a blank canvas, excel-like language
2. Model-driven: define tables and relationships, UI is generated
3. Power pages: external pages, not relevant here
4. Code apps: new (literally just released Feb 2026); developer writes code and deploy into their platform, inherits all IAM, connectors, governance.

Connectors: Salesforce, SQL, Excel, Stripe, can write custom wrapping any REST API
Dataverse: their relational database
Power Automate: approval engine -> sent to Teams (Devin can do)

#### Limitations
- Item limit is the most critical: non-delegable queries are capped at 2k records from connected data sources.
	- Anything past that is **silently ignored** - no error
	- Not all sources can delegate: Excel for instance CAN’T
- Reading or writing hundreds of data through connectors also can exceed limits
	- 1000 connector requests per **24 hour**
- Attachment control is limited to 50MB, can’t use S3 or other destinations

#### Pricing
- Costs $20 per seat. If the company is spending $250,000 then they have close to 1.5k users. For a series C startup that’s roughly the entire company.
- All of these people will be creating tickets to the engineering team.

## What Devin needs to achieve

Basic functionality is easy to achieve.
The following is where most of the Microsoft bill brings:
- Integrate smoothly with their Entra IDs
- Nicely-done authorization
- Audit logging
- Data loss prevention -> replicas
- SOC coverage

