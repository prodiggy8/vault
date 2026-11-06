---
tags:
type:
author:
description:
aliases:
date created: Thursday, November 5th 2026, 4:20:23 pm
date modified: Thursday, November 5th 2026, 4:20:26 pm
---
# Problem 1
Let the locations be $0, 1, \dots, n-1$, let $m$ be the number of orders, and write $d(u,v)$ for the travel time from $u$ to $v$. 

We build a network shaped like a grid. Each row is a location, each column is a minute $\tau = 0, 1, \dots, T$. One unit of flow will stand for one worker.

**Edges:**

- **Source and sink edges**
	- Capacity $k$
	- Cost $0$
- **Waiting edges** 
	- An edge $(v, \tau) \to (v, \tau + 1)$ 
	- Capacity $k$
	- Cost $0$
- **Travel edges** 
	- An edge $(u, \tau) \to (v, \tau + d(u,v))$
	- Capacity $k$
	- Cost $0$
- **Order edges** 
	- An edge $(a_i, t_i - d(a_i, b_i)) \to (b_i, t_i)$ 
	- **Capacity 1**
	- **Cost $-p_{i}$**

Run min-cost max flow from $s$ to $t$ on this network. Maximum profit is $-(\text{min cost})$.

**Flow → schedule.** 
Take an integral optimal flow; one exists by the integrality theorem. The graph is a DAG, so the flow splits into $k$ paths. Give one path to each worker and read it edge by edge:

- waiting edge: wait one minute,
- travel edge: move empty-handed,
- order edge: pick up order $i$ and deliver it at exactly $t_i$.

1. Worker carries something only while on an order edge, so they hold **one order at a time**.
2. Order edges have **capacity 1**, so **no order is done twice**.

**Schedule → flow.** Take a valid schedule and one worker, and list their orders in delivery order. Say the worker is at node $(u, \sigma)$: either $(0,0)$ at the start, or the drop-off point of their previous order. The next order $j$ is still feasible, and by the triangle inequality,

$$\sigma + d(u, a_j) + d(a_j, b_j) \le t_j .$$

So the path can do this: **travel** to $a_j$, then **wait** until minute $t_j - d(a_j, b_j)$ (the inequality says this wait is not negative), then take **order edge $j$** to $(b_j, t_j)$. After the last order, wait until minute $T$ and go to $t$. An idle worker just waits at location $0$. Each order is done at most once, so every capacity is respected, and the result is a flow of value $k$ with **cost $= -$profit**.

[IMPORTANT]

Both directions together give: min cost $= -$max profit.

Runtime: $n(T+1) + 2$ nodes and $O(n^2 T + m)$ edges, each built in $O(1)$. This is **polynomial in $n$, $m$, $T$**.

Detail:
The maximum flow value is exactly $k$. The edge out of $s$ has capacity $k$, and the path that waits at location $0$ from minute $0$ to minute $T$ and then goes to $t$ can carry all $k$ units by itself. So the algorithm returns a flow of value $k$ with the least cost. Asking for a maximum flow costs us nothing: any flow of smaller value can be increased to value $k$ by sending the missing units along that waiting path, which has cost $0$.
# Problem 2

We first pick a point for the searcher. The obvious choice is the centroid, but it doesn’t work. We try the circumcenter, which is equidistant from $a, b, c$.
$$
\begin{align}
\|O-a\|^2 &= \|O-b\|^2 \\
(x+1)^2 + y^2 &= (x-1)^2 + y^2 \\
x &= 0 \\
 \\
\|O-a\|^2 &= \|O-c\|^2 \\
1 + y^2 &= (y-2)^2 \\
y &= \frac{3}{4} \\
 \\
X &= \left( 0, \frac{3}{4} \right)
\end{align}
$$
$$\begin{align}
\|O-a\|^2 = \|O-b\|^2 = 1 + \tfrac{9}{16} = \tfrac{25}{16} \\ \|O-c\|^2 = \left(\tfrac54\right)^2 = \tfrac{25}{16}
\end{align}$$



**Upper bound: searcher's strategy.** Let $q$ be the pure strategy $Y = O$. By Claim 2 (a pure response is optimal), the evader's best reply is a pure point, so
$$\text{ub}(q) = \max_{x \in T} \|x - O\|^2.$$
The disk $\{z : \|z-O\| \le R\}$ is convex and contains $a, b, c$, hence contains their convex hull $T$. So $\|x - O\|^2 \le R^2$ for all $x \in T$, and $\text{ub}(q) = \tfrac{25}{16}$ (attained at any corner).

**Lower bound: evader's strategy.** Let $p$ put probability $\tfrac{5}{16}, \tfrac{5}{16}, \tfrac{6}{16}$ on $a, b, c$. Then
$$\mathbb{E}_p[X] = \tfrac{5}{16}(-1,0) + \tfrac{5}{16}(1,0) + \tfrac{6}{16}(0,2) = (0, \tfrac34) = O.$$
By Claim 2 the searcher's best reply to $p$ is a pure point $y$, so $\text{lb}(p) = \min_{y \in T} \mathbb{E}_p\|X - y\|^2$. For any $y \in T$, write $X - y = (X - O) + (O - y)$ and expand:
$$\mathbb{E}_p\|X-y\|^2 = \mathbb{E}_p\|X-O\|^2 + 2\,\mathbb{E}_p[X-O]\cdot(O-y) + \|O-y\|^2 = R^2 + 0 + \|O-y\|^2 \ \ge\ \tfrac{25}{16}.$$
The first term is $R^2$ because $X$ is always a corner, each at distance $R$ from $O$; the cross term vanishes because $\mathbb{E}_p[X] = O$. Equality holds at $y = O$, so $\text{lb}(p) = \tfrac{25}{16}$.

**Conclusion.** $\text{lb}(p) = \text{ub}(q) = \tfrac{25}{16}$, so the value of the game is $v = \tfrac{25}{16}$, with minimax-optimal strategies $p = (\tfrac{5}{16}, \tfrac{5}{16}, \tfrac{6}{16})$ on $(a,b,c)$ for the evader and $Y = O$ for the searcher.

# Problem 3

**Variables:**
- $x_{i,e}$ for each $1 \leq i \leq k$ and each $e \in E$. Amount of material $i$ sent on road $e$.
- $w_j$ for each $1 \leq j \leq \ell$

Define:
$$F(v) = \text{set of factories located at } v$$
$$
b_i(v) = \begin{cases} D_i & \text{if } v = s_i \\ 0 & \text{otherwise} \end{cases}
$$
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

- The LP has $k|E| + \ell$ variables and $|E| + k|V|$ constraints.
- Its size is polynomial in the input, so it can be solved in polynomial time.

