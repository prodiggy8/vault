---
tags:
type:
author:
description:
aliases:
date created: Monday, September 28th 2026, 11:43:32 pm
date modified: Tuesday, September 29th 2026, 12:11:49 am
---
The client's real question is the cost of app four through thirteen, not whether three apps can be built. Since the customer is looking to build much more, I decided to build a core structure so that they can easily add new dashboards: shared interface and primitives, auth, database, RBAC, audit logs, and then a Playbook you can use on Devin to create new modules (took about 1:20h).

Then I used this playbook in three parallel sessions to create the three dashboards: KYC, refunds, and feature-flag (30 minutes!). The foundation replaces Dataverse, Entra integration, auditing and governance, not the drag-and-drop canvas.

**Next.js**: I decided on a monolith application on Next because maintaining a microservices architecture or a monorepo is workload a company using PowerApps is not looking for. There is a `core/` folder and one `modules/<name>` folder per app. Each has a schema, actions, queries, pages, and one permission matrix (for the roles).

For the rest of the stack I chose standard tools: Postgres, Drizzle, Auth.js, and shadcn/ui.

**Audit:** every module always calls `withAudit(tx, ...)`, every action has an audit log in the same transaction. Integration tests assert that a rejected action writes no audit row and a successful one writes exactly one. This is to replicate PowerApps’ strong audit logs.

**Microsoft SSO:** Auth.js with the Entra provider against the consumer tenant issuer, so anyone can run the repo with their own Microsoft account. Roles live in Postgres with a seed-admin env var since personal Microsoft accounts (the ones I have access to for a test app registration) don’t carry group claims. Production will pin the issuer to the tenant and map Entra groups to roles.

**Server-side tables:** Filter, sort and pagination run in Postgres. This is an improvement over the PowerApps delegation limit on some sources like Excel and SharePoint. We could also easily attach an S3, which can’t be done in PowerApps either without custom code.

## Process

I wrote specs for each module and the playbook and reviewed PRs. Devin did 99% of the code. Some bugs surfaced and I kept a few in the deck e.g. an email linking flag that would have let a second Microsoft account inherit admin. That was important to mention because Devin still needs an engineer to review PRs and that could be workload the FinTech isn’t looking for.

## Tradeoffs

- As mentioned S3 for KYC documents wasn’t built due to lack of time. Read-access logging, audit export or retention weren’t in the scope for the same reason.
- The JWT callback hits Postgres on every request so a role change or disable takes effect immediately. If it’s a high demand dashboard that could be something to change later.
- I choose to spend a bit of the time on polish versus experiments due to slop UI.
- I choose to do parallel development over sequential; it was quicker but it costed race conditions.

## What I would change

- Use TDD with Devin; leaving tasks for a second session led to some major bugs.
- I would be more careful with race conditions; account for parallelism in the playbook.
- Add a small CI job running lint, typecheck and test:all.
- The way I was sharing knowledge between sessions was through a file in the repo. I should have used Knowledge, which I found out about post-prototype.