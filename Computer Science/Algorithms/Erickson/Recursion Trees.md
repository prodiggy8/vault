---
tags:
  - algorithms
type:
author:
description:
aliases:
date created: Sunday, August 2nd 2026, 8:05:48 pm
date modified: Sunday, August 2nd 2026, 8:06:02 pm
---
Given recursion $T(n)=rT\left( \frac{n}{c} \right)+f(n)$, we draw a r-ar tree where each node at depth $d$ contains $f\left( \frac{n}{c^d} \right)$.

The total complexity would be then $T(n)=\sum_{i=0}^L r^i  f\left( \frac{n}{c^i} \right)$, where $L$ is the depth of the tree.

Three common cases:
- **Decreasing:** if the series decays exponentially, i.e. every term is a constant factor smaller than the previous, then $T(n)=O(f(n))$.
- **Equal:** if all terms are equal, $T(n)=O(f(n) \cdot L)=O(f(n) \cdot \log n))$
- **Increasing:** If series grows exponentially, then $T(n)=O(r^L)=O(n^{\log_c r})$, the leaves dominate the tree.

Need to review: recursion trees, ignoring floors and ceilings