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

If it does, it starts being cheaper at $v$, so $c'(v) < c(v)$.
Pick $u$ that comes before:
- $c'(v) = c'(u) + \$'(u, v)$
- $c'(u) \geq c(u)$

Hence $c'(v) \geq c(u) + \$'(u, v)$.

Hence it must be that $\$'(u,v)$ changed. The only way the cost changes is if we used that path with a reverse edge. By definition:

- $\$'(u, v) = -\$(v, u)$
- $c'(v) \geq c(u) - \$(u, v)$
- Since we used the reverse edge


#### Does it output the minimum?
