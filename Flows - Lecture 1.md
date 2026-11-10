- Capacity constraint
- Conservation constraint

Want to maximize: $|f|=\sum_{u} f(s \to u) - \sum_{u}f(u \to s)$

### s-t paths

**Observation:** a flow is not optimal if there exists an s-t path with available capacity.

### s-t cuts

- A cut is a partition of the vertices into two disjoint sets $S$ and $T$ with $s \in S$ and $t \in T$.
- The capacity of the cut is the sum of the capacities of the edges from $S$ to $T$.

The **net flow** of a cut is the sum of flows from $S$ to $T$ minus flows from $T$ to $S$:
$$f(S \to T) = \sum_{u \in S} \sum_{v \in T} f(u \to v) - \sum_{u \in S} \sum_{v \in T} f(v \to u)$$
$|f|$ is equivalent to the net flow across **any cut**. No matter where you cut the graph, there’s still the same amount of flow making it from $s$ to $t$.

- The value of any s-t flow is $\leq$ value of any s-t cut.
- Hence, max flow $\leq$ minimum cut.
- Hence, any s-t flow $\leq$ max s-t flow $\leq$ minimum s-t cut $\leq$ any s-t cut.

If we can find a flow that is equal to the capacity of **any cut** then it must be maximum!

### Finding maximum flow

We define **residual capacity** which accounts for both the remaining capacity on an edge, but also adds the ability to undo bad decisions and redirect a sub optimal flow.

> [!Residual capacity]
> Given flow $f$ and $G$: 
> $$c_{f}(u, v)=\begin{cases}
> c(u, v) - f(u, v) & \text{ if } (u, v) \in E \\
> f(v, u) & \text{ if } (v, u) \in E
> \end{cases}$$
> The second case: if $f(v, u)$ has been sent down some edge $(v,u)$ we can undo that by sending flow in the reverse direction!

Residual graph: $G_{f}$ is directed graph with edges of positive residual capacity. This might include reverse-edges of original graph $G$!

- **Augmenting path:** path from $s$ to $t$ of non-zero residual capacity in the network.
#### Ford-Fulkerson 

```
while (there exists augmenting path):
	push the maximum possible flow along P
```

It might be some graphs have anti-parallel edges (both u, v and v, u). We can:
- disallow them
- combine both into a single edge with sum of capacities
- include pair of parallel edges in the residual graph

### Proof

Runs in $O(mF)$ time where $F$ is the value of maximum $s-t$ flow and each iteration does a DFS in $O(m + n)$, with $m \geq n - 1$ so $O(m)$.

- In the final residual graph, $s$ and $t$ must be disconnected.
- Let $S$ be vertices reachable from $s$ and $T$ otherwise
- e. $t$ must be in $T$ since disconnected so it’s a valid cut.
- $|f| = f(S, T) \leq cap(S, T)$

Claim: edges that cross the cut in $S \to T$ direction are at maximum capacity. Otherwise, then we could reach $T$ in the residual graph, which contradicts construction.

Claim: edges that cross the cut in $T \to S$ are empty. Otherwise, there would be a reverse edge with positive residual capacity from $S$ to $T$, contradicting construction.

- Hence, the net flow across the cut is equal to the capacity of the cut. **Hence the flow is maximum and the cut is minimum.**

**Integrality theorem:**
If all capacities are integer, there exists a maximum flow in which the flow on every edge is integer. The algorithm finds this one.

### Bipartite Matchings

**Bipartite graph** is a graph with vertices divided in two disjoint sets L and R such that so that every edge has one endpoint in L and the other in R.

**Matching** is a set of edges with no endpoints in common.

**Perfect matching** is if every point in L is connected to every point in R. **Maximum matching** is a matching with maximum possible number of edges.

```pseudo title="Matching Algorithm"
set source node s connected to all vertices in L
set sink node t connected to all vertices in R
give each edge capacity 1
run ford fulkerson
output edges with non-zero flow as the matching
```

**Proof reduction is correct:**
- Show that one way corresponds to another and vice versa.

