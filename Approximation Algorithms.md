---
tags:
  - algorithms
type: note
author:
description:
aliases:
date created: Friday, November 13th 2026, 11:36:59 am
date modified: Friday, November 13th 2026, 11:37:03 am
---
- Find a polynomial algorithm that gives a semi-optimal (within 10%) solution
- Find a faster algorithm than the naive one.

> [!definition] Approximation Algorithm
> Given an optimization problem with optimal value $\text{OPT}$ and algorithm that produces feasible solution $\text{ALG}$, we say the algorithm is a $c$-approximation algorithm if $\text{ALG}$ is **always** within a factor of $c$ of $\text{OPT}$.
> 
> **Minimization:** $c$-approximation ($c>1$) if for **all inputs**, $\text{ALG} \leq c \cdot \text{OPT}$
> **Maximization:** $c$-approximation ($0 < c < 1$) if for **all inputs** $\text{ALG} \geq c \cdot \text{OPT}$

# Problem 1

$m$ identical machines, want to schedule $n$ jobs. Each job has processing time $p_{i} > 0$. 
Minimize load of most loaded machine.

If $S_{j}$ is the set of jobs assigned to machine $j$, we minimize:
$$max_{1 \leq j \leq m} \sum_{i \in S_{i}}p_{i}$$
**Alternative definition**

$n$ blocks, block $i$ has height $p_{i}$.
Arrange into $m$ stacks such that we minimize the height of the shortest.

![[Approximation Algorithms.png]]

**Problem 1** Give a concise argument that makespan of 8 is optimal for the block stacking example above.

	Since we have 3 stacks and the sum of all blocks is 22, we must have height at least 22 / 3 = 7.33. Since we only have integer heights, the minimum height must be ceil(7.33) = 8.

### Algorithms

**Greedy**

Start with $m$ empty stacks, then for each block, place it in the shortest one so far.

> [!Theorem]
> The greedy approach outputs a solution with makespan at most 2 times the optimum.

Call last block added to tallest stack $i*$ with height $p_{i*}$ and remaining height of tallest stack $L$.
$\text{ALG} = L + p_{i*}$

We know $\forall i \; \text{OPT} \geq p_{i}$ including $i*$ since every block must be placed somewhere.
Since the algorithm chooses the *shortest stack*, $L$ was shortest!