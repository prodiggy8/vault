---
tags:
type:
author:
description:
aliases:
date created: Sunday, November 8th 2026, 6:52:22 pm
date modified: Sunday, November 8th 2026, 6:52:27 pm
---
We assume every vertex is reachable from $s$, so DFS and BFS are both $O(m)$.
### Edmonds-Karp

Ford-Fulkerson but selecting the **shortest** augmenting path each time.
At most $mn$ iterations, $O(nm^2)$.

*Proof:*

- distance $d$ from $s$ to $t$ in the residual graph never decreases.

Since shortest path, then $d_{v_{i}} = d_{v_{i-1}} + 1$.
Augmenting does:
1. Saturate one edge, disappears from residual graph. This can never decrease $d$.
2. We can add reverse edges $(v, u)$. Since $d_{v} = d_{u} + 1$, it doesn’t decrease $d$ either.

- every $m$ iterations, $d$ has to increase at least 1

Each iteration saturates one edge.
For it to be used again, only if its residual edge is used too.
But residual edge can only be part of shortest path if $d$ increased since $d_{v} = d_{u} + 1$.
Since there are $m$ edges, after $m$ iterations $d$ must have increased.

We can only increase $d$ up to $n$ times, so total $mn$.

### Dinic’s

**Layered graph:** Run BFS to find all distances $d_{v}$ from $s$ to $v \in V$. Lay them out in layers $0, 1, \dots, d$.
- Read original but ignore all edges that don’t satisfy $d_{v} = d_{u} + 1$

**Blocking Flow:** a flow such that every $s-t$ path has at least one edge that gets saturated.
- Maximum flow implies blocking but the opposite is not true.
- Think of as “maximal” flow

> [!Theorem] 
> Blocking flow can be found in $O(nm)$ time

Strategy:
- Find distances with BFS in $O(n+m)$
- Find augmenting paths with DFS
- Ignore dead ends for all future DFS runs

-> need to finish tomorrow
### Dinic’s on unit-capacity graphs




## Questions for tomorrow
- Why sometimes we use $O(m)$ and sometimes $O(m + n)$ for BFS and DFS
- Why exactly blocking flows?
- Read note on implementation



