---
tags:
type:
author:
description:
aliases:
date created: Wednesday, November 18th 2026, 5:26:42 pm
date modified: Wednesday, November 18th 2026, 6:06:13 pm
---

### Problem 1

First we calculate the net balance $b_{i}$ (collectibles minus debt) for each person $i$. While some person has a non-zero balance, repeat:

- Pick some person $p$ with positive net balance and some other $q$ with negative
- Have $q$ transfer $\min(b_{p}, -b_{q})$ to $p$.
- Update their balances accordingly

### Problem 2

##### a)

**Variables:**
For each $s-t$ path $p \in P$, let $f_p$ be the amount of flow sent along $p$.

**Maximize**: $$\sum_{p \in P} f_{p}$$
**Subject to:**
$$
\begin{aligned}
\sum_{p \in P \\ e \in p} f_{p} \leq c(e) && \forall e \in E \\
f_{p} \geq 0 && \forall p \in P
\end{aligned}
$$

##### b)

**Variables:**
Define $y_{e}$ for each edge $e \in E$

**Minimize:**
$$\sum_{e \in E} c(e) \cdot y_{e}$$
**Subject to:**
$$
\begin{aligned}
\sum_{e \in p} y_{e} \geq 1 && \forall p \in P \\
y_{e} \geq 0 && \forall e \in E
\end{aligned}
$$

