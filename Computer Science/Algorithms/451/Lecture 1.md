---
tags:
  - algorithms
  - computer-science
  - course/15-451
type: note
author:
description:
aliases:
date created: Tuesday, August 25th 2026, 1:26:30 pm
date modified: Tuesday, August 25th 2026, 1:26:32 pm
---

> [!definition] Average Cost
> This is equivalent to the *expected value* of its cost over a uniform distribution of possible inputs.

> [!definition] Expected Cost
> Maximum cost over all possible inputs to the algorithm, of the expected value of the cost of that input, where the expected value is over the distribution of random choices made by the algorithm.





[[Quicksort]]
[[Quickselect]]
[[Momselect]]

Need to study:
- Methods to solve recursions
- Expected value (GTI slides on probability)
- C++ STL
- Speed run graphs and DP with Erickson


### Problems

1. Find an increasing function $F: \mathbb{R}_+ \rightarrow \mathbb{R}_+$, such that $\mathbb{E}[F(i)] >> F(\mathbb{E}[i])$

$$X=n \text{ with probability } \frac{1}{n} \text{ and } X=0 \text{ otherwise}$$
$$F(x) = x^2$$
- $F(\mathbb{E}[X])=F(1 + 0)=1$
- $\mathbb{E}[F(X)]=\frac{1}{n} \cdot n^2 + \frac{n-1}{n} \cdot 0=n$

2. Show that for $c$ and $a_1,\dots,a_k$ such that $a_1 + \dots + a_k=1$ and each $a_i<1$, the recurrence $T(n) \leq T(a_{1} n) + T(a_{2} n) + \dots + T(a_{k} n)+cn$ solves to $O(n \log n)$. Fact: $T(n) = T\left( \frac{n}{2} \right) + T\left( \frac{n}{2} \right) + n$ solves to $T(n)=\Theta(n\log n)$.



### My problems

1. Prove that $\mathbb{E}[F(i)] = F(\mathbb{E}[i])$ if $F$ is linear
