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

Layered graph: every edge satisfies $d_{v} = d_{u} + 1$

```pseudo title="Dinic's"
repeat:
	run BFS on residual graph
	if t unreachable:
		return
	
	build layered graph
	push blocking flow with DFS
		kill dead edges
		no need to consider newly introduced back edges
```

**Line 1:** $O(n)$ iterations
**Line 5:** $O(n + m)$
**Line 6:** $O(nm)$

An augmenting path must contain at most $n-1$ edges otherwise we **repeat a vertex** which is pointless.

DFS takes $O(n+m)$ because we might visit **dead end edges** that don’t take us to $t$. We remove those forever when we see them. 

Cost for DFS with no dead edges to find $m$ augmenting paths because each augmentation saturates at least one edge.
$$
\begin{align}
=&\sum_{i = 0}^m n + \text{new edges marked dead} \\
=&nm + \sum_{i = 0}^m \text{new edges marked dead} \\
=&nm + m \\
=&O(nm)
\end{align}
$$
Since we can have at most





