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
Take an integral optimal flow. The graph is a DAG, so the flow splits into $k$ paths. Give one path to each worker and read it edge by edge:

- waiting edge: wait one minute,
- travel edge: move empty-handed,
- order edge: pick up order $i$ and deliver it at exactly $t_i$.

1. Worker carries something only while on an order edge, so they hold **one order at a time**.
2. Order edges have **capacity 1**, so **no order is done twice**.

**Schedule → flow.**
Take a valid schedule and one worker, and list their orders in delivery order. Say the worker is at node $(u, \sigma)$ and the next order is $j$. 
$$\sigma + d(u, a_j) + d(a_j, b_j) \le t_j .$$
So the path can do this: **travel** to $a_j$, then **wait** until minute $t_j - d(a_j, b_j)$, then take **order edge $j$** to $(b_j, t_j)$. After the last order, wait until minute $T$ and go to $t$. 

Each order is done at most once, so every capacity is respected, and the result is a flow of value $k$ with **cost $= -$profit**.

Runtime: $n(T+1) + 2$ nodes and $O(n^2 T + m)$ edges. This is **polynomial in $n$, $m$, $T$**.

# Problem 2

You want a spot that's close to everywhere in the triangle, because the evader will go to wherever is farthest from you. And where is farthest from a fixed point? Always a corner.
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



**Searcher's strategy.** 
 Searcher's strategy: stand at $O$.
 Circle around circumcenter is convex. circle's interior is convex. 
 
 Every point the evader could pick is within distance $R$ of $O$. The payoff is at most $R^2 = \tfrac{25}{16}$, always.

**Evader's strategy.** 
A corner is the farthest from wherever the searcher is so we go there.
 
Say the evader point has an average position $\mu$. Then:
$$
\mathbb{E}\|X - y\|^2 = \mathbb{E}\|X - \mu\|^2 + \|\mu - y\|^2
$$
 The squared distance from searcher is the evader's spread around his own average, plus the searcher's distance from that average. 
 
 The second term is the searcher's choice,best he can do is make it zero.
 
 The evader wants to maximize his spread around his own average. **Choosing the probabilities.** Here's the trick. Use the same identity with $y = O$: 
 
  The left side is at most $R^2$, because everything is within $R$ of $O$. So the spread is at most $R^2 - \|\mu - O\|^2$. To get the spread all the way up to $R^2$ you need two things: the average $\mu$ must be exactly $O$, and $X$ must always sit at distance exactly $R$ from $O$, which inside the triangle means only the corners. So we solve for weights on the corners whose average is $O$: $$p_a(-1,0) + p_b(1,0) + p_c(0,2) = (0, \tfrac34), \qquad p_a + p_b + p_c = 1.$$ The $x$-coordinate says $p_a = p_b$. The $y$-coordinate says $2p_c = \tfrac34$, so $p_c = \tfrac{6}{16}$. The rest is split evenly: $p_a = p_b = \tfrac{5}{16}$. Notice the top corner gets a bit more than a third. That's because $O$ sits above the center of mass of the triangle, so the top needs extra weight to pull the average up to it. **The evader's floor.** Evader's strategy: $a$ with probability $\tfrac{5}{16}$, $b$ with $\tfrac{5}{16}$, $c$ with $\tfrac{6}{16}$. The average is $O$. Every corner is at distance $R$ from $O$, so the spread is exactly $R^2$. By the identity, against any searcher point $y$, $$\mathbb{E}\|X - y\|^2 = \tfrac{25}{16} + \|O - y\|^2 \ge \tfrac{25}{16}.$$ Even if the searcher stands right on $O$, he can't push it below $\tfrac{25}{16}$. If he randomizes, every one of his possible points gives at least $\tfrac{25}{16}$, so the average does too. That's our floor.

Formula:
$$X - y = (X - \mu) + (\mu - y).$$
$$u = X - \mu$$
$$w = \mu - y$$
$$\|u + w\|^2 = \|u\|^2 + 2\,u\cdot w + \|w\|^2$$
$$\|X - y\|^2 = \|X - \mu\|^2 + 2\,(X - \mu)\cdot(\mu - y) + \|\mu - y\|^2$$
$$\mathbb{E}\|X - y\|^2 = \mathbb{E}\|X - \mu\|^2 + 2\,\mathbb{E}[X - \mu]\cdot(\mu - y) + \|\mu - y\|^2$$
$$E[X − μ] = E[X] − E[μ]$$
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

