---
tags:
  - algorithms
  - computer-science
  - course/15-451
  - amortized-analysis
type: note
author:
description:
aliases:
date created: Saturday, September 19th 2026, 5:12:16 pm
date modified: Saturday, September 19th 2026, 5:25:18 pm
---
Other resources: CLRS, Chapter 17

Amortized analysis applies over a *sequence of operations*

**Aggregate method**

We simply add the **total** cost of performing a sequence of $m$ operations and divide by $m$.

**Dynamic arrays**

- Doubling resizing, distinguish between capacity $c$ and size $n$
