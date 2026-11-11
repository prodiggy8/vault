---
tags:
type:
author:
description:
aliases:
date created: Monday, November 9th 2026, 1:49:45 am
date modified: Monday, November 9th 2026, 1:49:49 am
---
$$\operatorname{cost}(f)= \sum_{e \in E}\$(e)f(e)$$

**Residual graph**
- Same capacity
- Cost $\$(e)$ on forward edge and $-\$(e)$ for backward ones

**Augmenting path**
- We want the cheapest one
	- BFS doesn’t work with weights
	- Dijkstra doesn’t work with negative edge weights
	- Use Bellman-Ford

#### Does the algorithm terminate?
Only if no negative cycles.

> [!Lemma] The cheapest path never gets cheaper when augmenting

[Proof if time later]

> [!Corollary]
> If no negative cycles before, no negative cycles after.

The algorithm terminates!
Runtime:
- Every iteration, one unit of flow is augmented. Every iteration runs the Bellman-Ford algorithm that takes $O(nm)$.
- $O(nmF)$.
#### Does it output the minimum?

Claim: we can add flow to a cycle in the graph without affecting feasibility.
Augmenting cycles: $\Delta$ units of flow and $W$ cost of cycle. If $\Delta W$ negative, flow wasn’t optimal.

