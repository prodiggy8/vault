---
tags:
  - algorithms
type: homework
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Sunday, August 30th 2026, 12:01:32 pm
date modified: Sunday, August 30th 2026, 12:01:35 pm
---
##### 1.
###### a)
I have read the course and university policy on academic integrity

###### b)
```pseudo
PowerRanks(A[1..n]):
	B = []
	p = n
	
	For every k from 3^i, .., 3^3, 3^2, 3^1, such that k < n:
		
		B[i] = DeterministicSelect(A[1..p], k)
		p = Partition(A, B[i])
		
	return B
```

###### c)
