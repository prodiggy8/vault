---
tags:
type:
author:
description:
aliases:
date created: Wednesday, November 18th 2026, 5:26:42 pm
date modified: Wednesday, November 18th 2026, 9:15:13 pm
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

##### c)

### Problem 3
##### a)

Let $k=\lfloor\log_2 n\rfloor$ and give every job size $1$. Use $2^k$ machines first. Each of the remaining $n-2^k$ jobs gets its own machine and is eligible only for that machine. Since $m\ge n$, there are enough machines for them.

Let $S_0$ be the set of all $2^k$ main machines. In each phase $i=1,\ldots,k$, partition $S_{i-1}$ into $2^{k-i}$ disjoint pairs. Introduce one job per pair, eligible only for the two machines in that pair.

Both machines in each pair have load $i-1$, so greedy may choose either. Let $S_i$ contain the chosen machine from each pair. Every machine in $S_i$ now has load $i$. After phase $k$, $S_k$ contains a single machine with load $k$. Introduce one final job eligible only for that machine, increasing its load to $k+1$.

The phases introduce $\sum_{i=1}^{k}2^{k-i}=2^k-1$ jobs, and the final job brings the total to $2^k$. Including the $r$ additional jobs gives exactly $n$ jobs.

Now consider an optimal schedule. Assign each phase-$i$ job to the machine in its pair that greedy did not choose. These machines form $S_{i-1}\setminus S_i$. Since the pairs within each phase are disjoint, and these sets are disjoint across phases, each machine receives at most one job. Assign the final job to the single machine in $S_k$, and each additional job to its own machine. Thus $\mathrm{OPT}=1$.

Greedy therefore has makespan $k+1=\lfloor\log_2 n\rfloor+1 \ge \log_2 n\cdot\mathrm{OPT}$.