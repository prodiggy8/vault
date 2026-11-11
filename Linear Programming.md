---
tags:
type:
author:
description:
aliases:
date created: Thursday, October 22nd 2026, 12:30:03 pm
date modified: Tuesday, November 10th 2026, 10:49:26 am
---

## Lecture 1

- $x_{1}, \dots, x_{n} \in \mathbb{R}$ 
- Linear function (e.g. $2x_{1} - 3x_{2}$)
- $m$ linear inequalities (e.g. $3x_{1}+4x_{2} \leq 6$)

We find values for $x_{i}$’s that satisfy constraints and maximize or minimize the function.

- Inequalities can’t be strict ($<$ or $>$) otherwise no optimal solution
- Needs to be **real valued**

___
#### Maximum flow

**Variables:**

Set up variable $f_{u,v}$ for each edge’s flow

Maximize: $\sum_{u} f_{s,u} - \sum_{u} f_{u,s}$

Subject to:

- $0 \leq f_{u,v} \leq c(u,v)$ for all $f_{u,v}$
- $\sum_{v} f_{u,v} = \sum_{v} f(v, u)$ for all $f_{u,v}$ such that $u \neq s, v \neq t$

___
#### Minimum-cost maximum flow

1. Solve for maximum flow first, then set up a new linear program and add the constraint that flow must equal $f$, solving for cost.

2. Combine both objectives

$$\begin{align}
f &= \text{net flow} \\
C &= \sum_{(u, v) \in E} \$(u, v)f_{u,v}
\end{align}$$

We maximize $f - \epsilon C$ where $\epsilon$ is a very small constant such that it will only matter to tie break between two feasible flows!

3. Reduce to minimum cost circulation

We add edge with infinity capacity from $t$ to $s$ and make $s$ and $t$ satisfy conservation as well.

Minimize $\sum_{(u,v) \in E} \$(u,v)f_{u,v}$
Subject to:
$0 \leq f_{u,v} \leq c(u,v)$ for all $f_{u,v}$
$\sum_{u \in V}f_{u,v} = \sum_{u \in V} f_{v, u}$ for **all $v$**.

To reduce minimum cost maximum flow to minimum-cost circulation, we give the infinity capacity $t-s$ edge a very negative cost such as the negative sum of costs to encourage sending flow there.

___
#### 2-Player Zero-Sum Games

We define a variable $v$ such that our gain in each column must be at least $v$ (minimum). Then we maximize that variable

**Variables:**
Probabilities $p_{1}, \dots, p_{n}$
$v$

**Maximize** v
**Subject to:**
- $p_{i} \geq 0$ for all $i$
- $\sum_{i} p_{i} = 1$
- $\sum_{i}p_{i}m_{ij} \geq v$ for all columns $j$

#### Slides

- Maximize, not minimize
- Constraints are all $\leq$
- All variables are non negative (these do not count towards number of constraints)

**How to convert to standard form?**
- Negative objective if minimizing
- Multiply by $-1$ to convert $\geq$
- Convert $=$ into $\geq$ and $\leq$
- For $x_{i}$ that can be negative we convert to $x_{i} = x_{i+} - x_{i-}$ with $x_{i+},x_{i-} \geq 0$

**Convexity**

The feasible region $Ax \leq b, x \geq 0$ is a convex set

## Lecture 2

Each $n$ variable constraint divides $R^n$ in half, we call **half space**.

The intersection of all half spaces is called a **convex polytope**.

> [!Dual]
> maximize $c^T$x
> subject to $Ax \leq b$
> $x \geq 0$
> 
> minimize $b^Ty$
> subject to $A^Ty \geq c$
> $y \geq 0$

If the primal has $n$ variables and $m$ constraints, the dual has $m$ variables and $n$ constraints

>[!theorem] Weak Duality
>If $x$ is any feasible solution to the primal LP and $y$ is any feasible solution to the dual LP
>$$c^Tx \leq b^T y$$

> [!theorem] Strong duality
> If primal is feasible and bounded, then dual is feasible and bounded.
> If $x^*$ is optimal solution to primal, and $y^*$ is optimal solution to dual:
> $$c^T x^*=b^Ty^*$$


### Feasibility and boundedness

- If primal feasible and bounded -> dual must be too
- If primal (maximization) unbounded, since $c^Tx \leq b^T y$, we have $\infty \leq b^T y$ so the dual is infeasible.
- If dual (minimization) unbounded, $c^Tx \leq -\infty$, so the primal is infeasible.
- Only one of the two can be unbounded.

![[Linear Programming.png]]

#### Example with Zero-Sum Games

NEED TO DO TOMORROW!! UNDERSTAND MATRIX

## Lecture 3

A linear inequality in $n$ divides $R^n$ in two, we call **half space**.
The points that satisfy all inequalities in LP is called **convex polytope**.

**Convexity:** $\operatorname{Conv}(a, b) = \{\alpha a + (1 - \alpha)b | 0 \leq \alpha \leq 1\}$
- All the points on the straight line in $R^n$ between $a$ and $b$ 

A set of points $S$ in $R^d$ is **convex** iff for all $a,b \in S$ we have that $\operatorname{Conv}(a, b) \subseteq  S$.
- The straight line between points is inside the same set!

**Vertex:** if it’s unique optimal point for some objective function
	- The furthest point for some direction
	- “Corner points”
**Extreme point:** for any $v \neq 0$, at least one of $q + v$ or $q-v$ is not in $P$.
	- You can’t move in a direction and stay in $P$
	- A point that can’t be written as the average of two other points in $P$

They’re the same thing!

#### Matchings

For each edge we define $0 \leq x_{u,v} \leq 1$ 
Maximize: 
$\sum_{(u,v) \in E} x_{u,v}$
Subject to:
$\sum_{v \in \operatorname{out}(u)} x_{u,v} \leq 1$ for all $u$

This LP has a maximum $Z_{G}$. For a graph $G$ the maximum matching $M_{G}$ solves this LP, but it might be less than $Z_{G}$.
- The integer solutions are a subset of the space being considered. We call this **relaxation**.

>> $G$ is bipartite graph, $\text{MP}_{G}$ is a polytope. If $q$ is extreme point, then it has integer coordinates.

- Consider $G'$ subset of only non-integer values

- If cycle and add and subtract $\epsilon$ alternating to preserve sum. It’s so small all variables still less than 1. So it’s in the polytope and we can move in both directions. Not extreme point.

- If no cycle then it’s a tree. Endpoints don’t cancel out. Since endpoints in $G’$ (non-integer), they have only one edge touching them that is fractional (also in $G’$). The others must be 0 (if fractional should have been in $G'$, if integer, breaks constraint that says $\leq {1}$). So we have slack to add $\epsilon$ without breaking. Can move again, not extreme point.

### Algebraic

Vertices are intersections of constraints.

Another way to see LP solutions is to see **which subset** of constraints is tight (equal to something).

A **basic solution** is the intersection of $n$ linearly independent tight constraints.
It might not be feasible

___
Let $R$ be the subset of rows we want to intersect.

**Cramer’s rule:** $x_{i}=\frac{\det(A^i_{R})}{\det(A_{R})}$
where $A_{R}^i$ means substitute column $i$ with the vector $b_{R}$.

**When is this guaranteed to be an integer?**
- All entries of $A$ and $b$ to be integers
- $\det(A_{R})=\pm 1$

**Unimodular:** square integer-valued with determinant $1$ or $-1$

We want $A_R$ to be unimodular for **any choice of rows R**

**Totally unimodular:** if every square submatrix determinant is 1, -1, 0

>> A linear program with polytope $Ax \leq b, x \geq 0$ where $A$ is totally unimodular and b is integral has only integral vertices.




FOR TOMORROW:
- Min cost max flow lecture!
- Game theory: lower bound and example
- Exercises:
	- Game theory recitation
	- LP recitation
	- Practice exam
	- Practice Claude exam
	- Cheat Sheet

Perception

Reasoning with data only after exam
Distributed only after exam