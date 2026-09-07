---
tags:
  - algorithms
  - computer-science
  - course/15-451
type: note
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Monday, September 7th 2026, 1:32:14 pm
date modified: Monday, September 7th 2026, 1:32:24 pm
---
## Word RAM model

- We have unlimited registers each storing a $w$-bit word
- Reading, writing, arithmetic, and logic operations on a **constant** number of words is free
- With input size $n$, we need $w \geq \log n$

For the last assumption: otherwise we wouldn’t be able to write $n$ as an index.

Example: multiplying $n$ integers, each $w$ bits long. The result would occupy $nw$ bits, that is, $n$ registers. We can only multiply a constant number of words in constant time, so this would take much more than $O(n)$.

Example: search in sorted array. In comparison model, we get $\Omega(\log n)$. In integer model, we get $O(1)$, we can just use the index of the desired element, $k$.





