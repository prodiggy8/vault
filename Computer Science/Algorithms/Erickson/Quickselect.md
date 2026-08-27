---
tags:
  - algorithms
type:
author:
description:
aliases:
date created: Sunday, August 2nd 2026, 8:14:00 pm
date modified: Sunday, August 2nd 2026, 8:14:05 pm
---
```pseudo
QuickSelect(A[1..n], k):
	if n = 1:
		return A[1]
	else:
		p = Pivot()
		r = Partition(A[1..n], p)
		if k < r:
			return QuickSelect(A[1..r-1], k)
		else if k > r:
			return QuickSelect(A[r+1..n], k)
		else:
			return A[r]
```

#### Analysis

$T(n) \leq n-1+ \mathbb{E}_{X}[T(X)]$
$\mathbb{E}_{X}=\sum_{x=1}^{n-1}Pr[X=x] \cdot T(x)$
$\mathbb{E}_{X} \leq Pr\left[ X \leq \frac{3n}{4} \right] \cdot T\left( \frac{3n}{4} \right) + Pr\left[ \frac{X>3n}{4} \right] \cdot T(n)$
	We divide