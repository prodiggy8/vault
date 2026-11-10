---
tags:
type:
author:
description:
aliases:
date created: Thursday, October 22nd 2026, 12:30:03 pm
date modified: Thursday, October 22nd 2026, 12:30:06 pm
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


