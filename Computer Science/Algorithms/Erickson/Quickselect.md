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

