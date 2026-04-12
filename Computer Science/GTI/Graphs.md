**Handshake Lemma:** $\sum_{v \in V}deg(v) = 2m$
- Sum of degrees is even
- Sum of odd degrees is even

Every connected graph with $n$ vertices has $\ge n - 1$ edges (by removing and adding vertices)
$G$ is acyclic if and only if every two vertices have $\le 1$ path between them
Every acyclic graph with $n$ vertices has $\le n-1$ edges (by induction, remove edge, break in two)

$A^l[u, v] =$ number of walks of length $l$ between $u$ and $v$

**Eulerian:** every edge once
**Hamiltonian:** every vertex once

**Theorem:** a connected graph has an Eulerian circuit if and only if every vertex has even degree

Graphs are **isomorphic** if there exists $\pi: V \rightarrow V'$ which preserves adjacency (NP but not NP-hard)

Every connected planar graph with $n$ vertices, $m$ edges, and $f$ faces satisfies: $n-m+f=2$
In a connected planar graph with $n \ge 3$ vertices and $m$ edges: $m \le 3(n-2)$
In a *bipartite* connected planar graph with $n \ge 3$ vertices and $m$ edges: $m \le 2(n-2)$

Every graph with max degree $\le D$ needs $\le D + 1$ colors
Every planar graph needs $\le 4$ colors

A tree is a connected acyclic graph.
1. $G$ is connected and $m=n-1$
2. $G$ is acyclic and $m=n-1$
3. Every two vertices in $G$ have exactly one path between them
4. $G$ is acyclic and adding any edge creates a cycle

$K_n$ has $n^{n-2}$ distinct trees

Prim's $O(n^3)$
Kruskal's $O(m \log m + n^2)$

Matching: set of edges where no two edges share an endpoint
Maximal: no edge can be added
Maximum: no matching has more edges

Any graph with a Hamiltonian cycle has a perfect matching

**Edge-ripping (maximal bipartite matching):** 
	while edges exist in $G$
		add to $M$
		remove endpoints from $G$

**Hungarian Method (not going to be included)**

**Perfect Matching**
If a bipartite graph $G$ has a matching that covers $X$, then:
$\forall S \subset X: |S| \le |N(S)|$
