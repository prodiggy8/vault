---
tags:
  - software
type: note
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Monday, September 28th 2026, 5:56:43 pm
date modified: Monday, September 28th 2026, 5:56:44 pm
---
Prompts:
- Include scope and domain clearly
- Step-by-step instructions (break down work in logical parts)
- Define success criteria
- References existing patterns and Code

**Be opinionated, not vague**
**Provide examples, templates, modules, resources**
**MCP for design, DBs, etc**
**Frequent feedback**

Decisions:
- NextJS -> no microservices, no separate backend/frontend, no monorepo, we need simplicity as PowerApps is simple.
- Microsoft SSO -> inherits structure already known to company
- Shared infra and DB -> can create multiple modules.
- Role-based access: again trying to fit MS’s shoes
- 