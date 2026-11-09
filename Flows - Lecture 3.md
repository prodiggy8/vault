---
tags:
type:
author:
description:
aliases:
date created: Monday, November 9th 2026, 1:49:45 am
date modified: Monday, November 9th 2026, 1:49:49 am
---
Same as normal flow but each edge has a cost $\$(e)$.
$$\operatorname{cost}(f)= \sum_{e \in E}\$(e)f(e)$$
**Residual graph**
- Same capacity as original
- Cost $\$(e)$ on forward edge and $-\$(e)$ for backward ones

**Augmenting path**
- Use Bellman-Ford to find paths since we allow negative edges
- Implement Ford-Fulkerson by selecting cheapest augmenting path

The shortest path only exists if there is no negative cycles, so we must prove the algorithm creates none.

**Lemma:** the cheapest path never gets cheaper
- Assume there’s a cheaper one
- $v$ is the first place where it’s cheaper, $c'(v) < c(v)$
- $u$ comes before, so $c'(v) = c'(u) + \$_{f'}(u, v)$
- $v$ is earliest, so $c'(u) \geq c(u)$ and $c'(v) \geq c(u) + \$_{f'}(u, v)$

Hence it must be that the residual cost $\$_{f'}(u,v)$ changed, otherwise we get contradiction.
If it changed, then the algorithm used the reverse edge and $\$_{f'}(u,v)=-\$_{f}(u,v)$.
$$
\begin{align}
c'(v) \geq c(u) - \$_{f}(u,v) \text{ but } 
\end{align}
$$