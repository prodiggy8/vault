### Flows

An s-t flow is a function $f: E \to \mathbb{R}$ that satisfies the following for every vertex $v$ except $s$ and $t$
$$\sum_{u}f(u \to v) = \sum_{v}f(v\to w)$$
Flow in, flow out.

Define:
$$
\begin{align} \\
|f| = \sum_{w} f(s \to w) - \sum_{u}f(u \to s) \\
\partial f(v) = \sum_{u} f(u\to v) - \sum_{u}f(v\to w)
\end{align}
$$
The net flow out of any vertex. By conservation, it’s 0 everywhere but $s$ and $t$.

Another function $c$ that assigns **capacity** to each edge. Flow is feasible if $0 \leq f(e) \leq c(e)$ for every $e$.

### Cuts

An s-t cut is a partition of the vertices into disjoint subsets $S$ and $T$.
The **capacity** of a cut is the sum of the capacities of the edges