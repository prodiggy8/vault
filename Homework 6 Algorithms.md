---
tags:
type:
author:
description:
aliases:
date created: Thursday, November 5th 2026, 4:20:23 pm
date modified: Thursday, November 5th 2026, 4:20:26 pm
---
We model this as a flow, with one commodity per material and one extra variable per factory for its widget output.

**Variables:**
- $x_{i,e} \ge 0$ for each material $i \in \{1,\dots,k\}$ and each edge $e \in E$: the amount of material $i$ sent along road $e$.
- $w_j \ge 0$ for each factory $j \in \{1,\dots,\ell\}$: the number of widgets produced at factory $j$.

**Notation.** For $v \in V$, let $\delta^{\text{in}}(v)$ and $\delta^{\text{out}}(v)$ be the sets of edges entering and leaving $v$. Let
$$
b_i(v) = \begin{cases} D_i & \text{if } v = s_i \\ 0 & \text{otherwise} \end{cases}
$$
and let $F(v) = \{\, j : f_j = v \,\}$ be the set of factories located at $v$. It may be empty or have several elements.

**LP:**
$$
\begin{aligned}
\text{maximize} \quad & \sum_{j=1}^{\ell} w_j \\
\text{subject to} \quad & \sum_{i=1}^{k} x_{i,e} \le u_e && \forall e \in E \\
& \sum_{e \in \delta^{\text{out}}(v)} x_{i,e} + \sum_{j \in F(v)} r_{ij}\, w_j \le b_i(v) + \sum_{e \in \delta^{\text{in}}(v)} x_{i,e} && \forall i \in \{1,\dots,k\},\ \forall v \in V \\
& x_{i,e} \ge 0 && \forall i \in \{1,\dots,k\},\ \forall e \in E \\
& w_j \ge 0 && \forall j \in \{1,\dots,\ell\}
\end{aligned}
$$

We output the optimal objective value.

**Explanation.**
- The first constraint is the shared capacity: on road $e$, all $k$ materials together can carry at most $u_e$.
- The second constraint is conservation of each material at each vertex. Material $i$ that leaves $v$, either shipped onward or used by the factories at $v$, can be at most what is available at $v$: the supply $D_i$ if $v = s_i$, plus whatever arrives at $v$. So for factory $j$ to produce $w_j$ widgets, $r_{ij} w_j$ units of each material $i$ must reach $f_j$.
- The constraint uses $\le$ instead of $=$ because unused material is allowed to stay where it is. Using equality with a nonnegative slack variable for each pair $(i, v)$ gives the same optimum.
- Several cases need no extra handling: several materials sharing a warehouse vertex, a factory sitting at a warehouse, and several factories at one vertex.
- The LP has $k|E| + \ell$ variables and $|E| + k|V|$ constraints, not counting nonnegativity. Its size is polynomial in the input, so it can be solved in polynomial time.