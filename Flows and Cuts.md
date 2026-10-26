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
date modified: Saturday, October 17th 2026, 1:11:47 pm
---

### Flows

A flow is a function $f: E \to \mathbb{R}$ that satisfies the following **conservation constraint** at every vertex except source $s$ and sink $t$.
$$
\sum_{u}f(u\to v)=\sum_{w}f(v \to w)
$$
The value of the flow $f$ denoted $|f|$ is the total net flow out of the source:

$$|f|=\sum_{w}f(s\to w) - \sum_{u}f(u\to s)$$

Now we define a capacity function $c: E \to \mathbb{R_{\geq 0}}$. We say flow $f$ is **feasible** if $0 \leq f(e) \leq c(e)$. The maximum flow problem is to compute a feasible flow whose value is as large as possible.

### Cuts

A cut is a partition of the vertices into disjoint subsets $S$ and $T$ where $s \in S$ and $t \in T$. The **capacity of a cut** is the sum of the capacities of the edges starting in $S$ and ending in $T$:

$$||S,T|| = \sum_{v \in S} \sum_{w \in T}c(v\to w)$$

The **minimum cut problem** is to compute a cut whose capacity is as small as possible!

> [!lemma] 
> The value of $f$ must be at most the capacity of minimum cut $(S, T)$.



