---
tags:
  - algorithms
  - computer-science
  - graph-theory
type: note
author:
description:
aliases:
date created: Wednesday, October 7th 2026, 10:42:17 am
date modified: Wednesday, October 7th 2026, 11:42:04 am
---

## Shortest Path 

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

```pseudo
D[v][0] = 0 if v = s else infinity

for k = 1 to n - 1: (path up to this weight)
for each v in V:
	D[v][k] = min(D[v][k-1], min for each neighbor u D[u][k-1] + w(u, v))
```

Total time is $O(mn)$.

We find the shortest **length**, but what about the shortest path?

- Instrument the array with additional array of parent pointers

Work backwards:

- if at vertex $v$ move to $x$ such that $d[v]=d[x] + w(x,v)$. Reconstruct path in $O(m + n)$ time.
___

Detect negative cycles reachable from $s$.

- Run the algorithm
- Path from $s$ to $v$ is at most $n-1$ edges long (if longer, some edge counted twice—cycle)
- Additional pass (n): some distance changed –> negative cycle.

## All-pairs Shortest Paths

If we use Bellman-Ford for each node it would be $O(mn^2)$.

### Matrix Products

$A[i,i] = 0$ for all i

$A[i,j]=w(i,j)$ if there exists $(i,j) \in E$

$A[i, j] = \infty$ otherwise

Just a matrix for shortest path from $i$ to $j$ with one or less edges.

- We try to make it two or less

$$B[i,j]=\min_{k}(A[i,k] + A[k,j])$$

This is just $A \cdot A$ but substituting $\cdot$ with $+$ and $+$ with $\min$.

To use four or less we can just do $B \cdot B$.

It becomes a binary search in $O(n^3 \log n)$. Doesn’t work with negative cycles (we need path to stop changing at some point). 

### Floyd-Warshall

Instead of increasing the number of edges in the path, we’ll increase the vertices we allow as intermediate notes.

```pseudo
// After each iteration of the outside loop, A[i][j] is length of the
// shortest i->j path that's allowed to use vertices in the set 1..k
for k = 1 to n do:
	for each i,j do:
			A[i][j] = min(A[i][j], (A[i][k] + A[k][j]))
```

### Dijkstra’s

If we have no negative edges, we run Dijkstra’s $n$ times, once at each vertex.

This runs in $O(n(n+m)\log n)$ which is great if graph is sparse.

*How to make it handle negative edge lengths?* 

- We compute potentials $\Phi_{v}$
- If $\exists(u,v) \in E$  
- 