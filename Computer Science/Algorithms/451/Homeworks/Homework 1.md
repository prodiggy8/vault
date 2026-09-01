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
```pseudo
PowerRanks(A[1..n]):
	B = []
	p = n
	
	For every k from 3^i, .., 3^3, 3^2, 3^1, such that k < n:
		
		B[i] = DeterministicSelect(A[1..p], k)
		p = Partition(A, B[i])
		
	return B
```



1. 
2. **Shuffle**
	1. {a}

```pseudo
SplitBitonic(A[1..n]):
	Let D, E be unbounded empty collections
	prev = negative infinity
	
	for every x in A:
		if x < prev:
			Prepend x to E
		else:
			prev = x
			Append x to D
			
	return D, E
```

**Correctness**

We assume $A[1..m]$ for some $m$ is sorted and $A[m+1..n]^R$ is sorted. Also, let $i$ be the first index where $A[i] < \text{prev}$.

Before step $i$, every step  of the loop in line 5 takes the else branch, so each $A[i]$ is appended to $D$ and $\text{prev}$ is always the last element of $D$, namely $A[i-1]$. Hence, the else condition is $A[i] \geq A[i-1]$ and $D$ non-decreasing.

Since $A[1..m]$ is non-decreasing, $i$



**Complexity**

We perform $n-1$ comparisons between `x` and `prev` in this algorithm, hence, it runs in $O(n)$.

2a
3b