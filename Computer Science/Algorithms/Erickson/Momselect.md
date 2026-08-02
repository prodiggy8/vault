---
tags:
  - algorithms
type:
author:
description:
aliases:
date created: Sunday, August 2nd 2026, 8:16:09 pm
date modified: Sunday, August 2nd 2026, 8:16:14 pm
---
```pseudo
MomSelect(A[1..n], k):
	if n < 25:
		use brute force
	else:
		m = ceil(n/5)
		for i in [1..m]:
			M[i] = MedianOfFive(A[5i-4..5i])
		mom = MomSelect(M[1..m], )
```