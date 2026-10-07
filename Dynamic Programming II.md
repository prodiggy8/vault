---
tags:
type:
author:
description:
aliases:
date created: Wednesday, October 7th 2026, 10:42:17 am
date modified: Wednesday, October 7th 2026, 10:42:19 am
---
**Dijkstra’s**

Given a direct graph $G=(V,E)$ with positive edge weights, the single-source shortest path problem can be solved in $O(m \log n)$ using heaps.

Using Fibonacci heaps, we could implement in $O(m + n \log n)$.

**Bellman-Ford**

This works for negative weights too.
In terms of DP, not functional programing.

1. For each node $v$, find length of shortest path from $s$ that uses at most $0$ edges, or $\infty$ if no such path exists. 

This yields $0$ if $v=s$, otherwise $\infty$.

3. The shortest path from $s$ to $v$ that uses $k$ or fewer edges will first go to some neighbor $x$ of $v$ using $k-1$ or fewer, then use $(x, v)$ to go to $v$.

We already know $k-1$ for all neighbors!
Take $\min$ over all neighbors of $v$ plus one.
Notice $s$ has no predecessors, so we don’t consider neighbors, just $dp[s]$.
The only case where it’s not $0$ is if there is a negative cycle passing through $s$.

$$d_k(v) = \min( d_{k−1}(v), \min_{(x, v) \in \operatorname{Neighbors(v)}} d_{k−1}(x) + w(x, v) )$$

Final answer: $D(v, n-1)$ finds shortest path from $s$ to $v$.

Total time is $O(mn)$.


