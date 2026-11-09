---
tags:
type:
author:
description:
aliases:
date created: Sunday, November 8th 2026, 6:52:22 pm
date modified: Sunday, November 8th 2026, 6:52:27 pm
---
### Edmonds-Karp

This algorithm runs Ford-Fulkerson by selecting the **shortest** augmenting path each time.
It makes it at most $mn$ iterations, and hence $O(nm^2)$.

- distance $d$ from $s$ to $t$ in the residual graph never decreases.

Since shortest path, then $d_{v_{i}} = d_{v_{i-1}} + 1$.
Algorithm can do two things:
1. Saturate one edge and it disappears from the residual graph. This doesn’t decrease $d$.
2. We can add reverse edges $(v, u)$. Since $d_{v} = d_{u} + 1$, such edge doesn’t create a shorter path either.

- every $m$ iterations, $d$ has to increase at least 1

Each iteration fills at least one edge. For it to be used again, it must be the reverse edge was used, which means that edge is part of the shortest path. Since $d_{v} = d_{u} + 1$ a reverse edge can only be in the shortest path if $d$ increases. Since there are $m$ edges, it follows the claim.

Since each $m$ iterations it increases, it can only increase $n$ (max distance is n). So $nm$ iterations.

### Dinic’s

**Layered graph**

Run BFS to find all distances $d_{v}$ from $s$ to $v \in V$.
Lay them out in layers $0, 1, \dots, d$ 
- There can’t be an edge from layer $i$ to $> i + 1$ otherwise the distance is wrong
- There can be edges that go back, but they are never part of shortest path

**Blocking Flow**

It’s a **flow in network $H$ such that every path in $H$ has at least one edge that gets saturated**

- A collection of paths that saturate at least one edge of every possible path in the network.
- Can be thought informally as a “maximal” flow


