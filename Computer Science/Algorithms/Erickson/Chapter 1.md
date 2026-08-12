---
tags:
  - algorithms
type:
author:
description:
aliases:
date created: Tuesday, August 11th 2026, 9:16:57 pm
date modified: Tuesday, August 11th 2026, 9:17:00 pm
---
**Idea:**
$$(10^na+b)(10^mc+d)=10^{2m}ac+10^m(bc + ad)+bd$$
Instead of multiplying two $n$ digit numbers, we divide and conquer by performing 4 multiplications with numbers of size $m=\frac{n}{2}$ digit.

```pseudo
SplitMultiply(x, y, n):
	if n = 1:
		return xy
	else:
		m = n / 2
		a = x / 10^m; b = x mod 10^m
		c = y / 10^m; d = y mod 10^m
		ac = SplitMultiply(a, c, m)
		bd = SplitMultiply(b, d, m)
		bc = SplitMultiply(b, c, m)
		ad = SplitMultiply(a, d, m)
		return 10^2m * ac + 10^m(bc + ad) + bd
```

This algorithm’s recursion writes as $T(n)=4T\left( \frac{n}{2} \right)+O(n) \in O(n^2)$

We can improve upon this algorithm by noting only three multiplications must be performed, because the middle coefficient $bc+ad$ can be computed from the other two, given by the following:
$$ac+bd-(a-b)(c-d)=bc+ad$$

```pseudo
FastMultiply(x, y, n)
	if n = 1:
		return xy
	else:
		m = n / 2
		a = x / 10^m; b = x mod 10^m
		c = y / 10^m; d = y mod 10^m
		ac = SplitMultiply(a, c, m)
		bd = SplitMultiply(b, d, m)
		co = SplitMultiply(a - b, c - d, m)
		return 10^2m * ac + 10^m * (ac + bd - co) + bd
```

This algorithm gives the recursion $T(n)=3T\left( \frac{n}{2} \right)+O(n) \in O(n^{\log{3}})$.


