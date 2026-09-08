---
tags:
  - algorithms
  - course/15-451
  - computer-science
type: note
author:
description:
aliases:
date created: Tuesday, September 8th 2026, 10:28:43 am
date modified: Tuesday, September 8th 2026, 10:29:00 am
---
References:
- DPV Chapter 1.5
- CLRS Chapter 11

**Static case:** lookup
**Incremental case:** lookup and inserting
**Dynamic case:** lookup, inserting, and deleting

Assume universe $U=0,\dots, u-1$ and size $u = 2^w$.
Keys are $S \subset U$ with $n=|S|$, with function $h: U \rightarrow \{0,\dots,m-1\}$.
We want $A[h(x)] = x$.

We use hash functions so not to have an array of size $u$. This introduces **collisions**, when $h(x) = h(y)$ for different $x$ and $y$. We assume separate chaining for this lecture.

**Desired properties:**
- Keys are spread out so we don’t have many collisions
- $m=O(n)$
- $h$ is fast to compute

**Claim:** for any $h$, if $u \geq (n-1)m+1$, there exists $n$ items that hash to the same location.

**Proof:** contrapositive. If every location had at most $n-1$ items, then $U$ could have size at most $m(n-1)$.

## Universal Hashing

> [!definition]
> A set $H$ where each $h \in H$ maps $U \rightarrow \{0,\dots,m-1\}$ is called **universal** if for all $x \neq y$ in $U$, we have:
> $$\Pr_{h \in H} [h(x) = h(y)] \leq \frac{1}{m}$$

Alternative way of defining: count the number of hash functions in $H$ that cause $x$ and $y$ to collide.
$$\frac{|\{h \in H | h(x) = h(y)\}|}{|H|} \leq \frac{1}{m}$$
