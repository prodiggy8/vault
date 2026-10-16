---
tags:
  - algorithms
  - course/15-451
type: note
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Wednesday, October 14th 2026, 1:49:41 am
date modified: Wednesday, October 14th 2026, 1:49:45 am
---
**Setup:** a directed graph $G$ with source $s$ and sink $t$, each edge has a capacity $c(e) \geq 0$. We want to push as much *flow* as possible from $s$ to $t$.

- $0 \leq f(e) \leq c(e)$
- Conservation: the same amount of flow going in must go out

How to know if a flow is not optimal?
A flow is not optimal if there exists an $\text{s-t}$ **path with available capacity.**

How can you see if a flow is indeed maximum?
