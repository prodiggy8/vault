---
tags:
  - algorithms
  - course/15-451
type:
author:
description:
aliases:
date created: Tuesday, September 22nd 2026, 12:30:57 pm
date modified: Tuesday, September 22nd 2026, 12:31:23 pm
---
> [!warning] Recall
> Kruskal: sort edges by weight and scan. Add to current forest if $u, v$ are not already connected.
> Takes $O(|E|\log|E|)$

#### Union-Find Problem

Disjoint sets
Representative element to identify it

`MakeSet(x)` creates new set with $x$
`Find(x)` find representative element of set containing $x$
`Union(x, y)` forms a new set that is the union of sets containing $x$ and $y$

**Kruskal:** we `MakeSet(u)` $\forall u (u \in G)$. For each edge we find the set of the vertices. If same, we skip. If not, we union. We’ll make $|V|$ sets, perform $|V|-1$ unions and $2|E|$ finds.

- Maintain representative manually: $O(n)$ union and $O(1)$ find.
- Graph with adjacency list: $O(1)$ union and $O(n)$ find.
- Tree: store parent pointer for each node.
	- `p(x) = x` for new set
	- $\operatorname{Union}(x, y) = p(\operatorname{find}(y)) = \operatorname{find}(x)$
Long chains make it innefficient
- Idea: always make the smaller tree a child of the larger
- Keep $s(x) = \text{size of } x$

Another optimization: path compression
- When finding, point every node along the path at its current root
- `Find(x): if p(x) != x: p(x) <- find(x) ...`

> [!lemma] Light lemma
> Any root-to-leaf path there are at most $\log n$ light nodes.

*Proof about complexity of the above*.

Find costs # nodes touched = 1 + light + heavy
= 1 + log n + heavy
So amortized cost is = 1 + log n + heavy + $\Delta \Phi$. We want $\Delta \Phi \approx -$heavy.

- A node can only heave **one** heavy children at a time by definition
- A heavy node can only halve it’s size (by compressing heavy node) $\log(\operatorname{size}(u))$ times. Hence $\Phi(F)=\sum_{u \in F}\log(\operatorname{size}(u))$.

Now the actual analysis using this function:

- **Makeset:** initially empty, so only actual cost: 1
- **Link:** linking node $y$ to node $x$
	- `size(x) >= 1` hence potential $0$
	- `size'(x) <= n` hence potential $\log n$
	- Hence change in potential is at most $\log n$. Costs $1+ \log n$

- **Find:** 
