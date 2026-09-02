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

We assume $A[1..m]$ for some $m$ is sorted and $A[m+1..n]^R$ is sorted. Assume there exists an $i$ such that it is the first index where $A[i] < \text{prev}$.

For all $j<i$, every iteration of the loop appends $A[j]$ to $D$ and $\text{prev}$ becomes $A[j]$. Thus, $D=A[1..i-1]$ and $\text{prev}=A[i-1]$. Since $A[i]<A[i-1]$, the sequence stopped increasing, so $i-1 \geq m$ and $A[i-1]$ is the maximum of $A$. Hence, $D$ is a prefix of a bitonic sequence up to its maximum, so $D$ is sorted.

For every $j \geq i$, $A[j] < A[i-1] = \text{prev}$ by assumption, so $A[j]$ is *prepended* to $E$ and $\text{prev}$ never changes. Thus, $E=A[i..n]^R$. By assumption, this segment is sorted and hence so is $E$.

Concatenating $D$ and $E^R$ is equivalent to concatenating $A[1..i-1]$ and $A[i..n]$ which is $A$, so we correctly decomposed $A$ in two sorted sequences as intended.

In the case no such $i$ exists, then $i=n+1$ by the end of the loop and $D=A, E=\emptyset$, which trivially concatenates to $A$.

**Complexity**

The loop performs one comparison per element, so $O(n)$ comparisons in total.

	2. {a}

```pseudo
Merge(A[1..n], B[1..m]):
	i = 1, j = 1, len = n + m
	for k from 1 to len:
		if j > m:
			C[k] = A[i]
			i++
		else if i > n:
			C[k] = B[j]
			j++
		else if A[i] < B[j]:
			C[k] = A[i]
			i++
		else
			C[k] = A[j]
			j++
	return C

SortBitonic(A[1..n]):
	D, E = SplitBitonic(A[1..n])
	return Merge(D, E)
	
```


3. 
	3. {a}

