---
tags:
  - algorithms
type:
author:
description:
aliases:
date created: Sunday, August 2nd 2026, 7:57:45 pm
date modified: Sunday, August 2nd 2026, 7:57:53 pm
---
```pseudo
QuickSort(A[1..n]):
	if n > 1:
		p = Pivot()
		r = Partition(A, p)
		QuickSort(A[1, r - 1])
		QuickSort(A[r + 1, n])
		
Partition(A[1..n], p):
	Swap(A[p], A[n])
	l = 0
	for i in [1..n-1]:
		if A[i] < A[n]:
			l++
			Swap(A[l], A[i])
	
	Swap(A[n], A[l+1])
	return l+1
```

There are many different ways to partition an array around a pivot. The version above is attributed to Nico Lomuto. $l$ counts the number of items lesser than the pivot.

### Complexity

$$
\begin{gather}
T(n)=T(r-1) + T(n-r) + O(n) \\ \\
\text{If we can guarantee the pivot is the median:} \\
T(n)=2T\left( \frac{n}{2} \right) +O(n) \in O(n \log n) \\ \\
\text{Else:} \\
T(n)=max_{1\leq r\leq n} \; \; T(r-1)+T(n-r)+O(n) \\
\end{gather}
$$

In the worst case, the two subproblems are completely unbalanced and we have $n$ iterations, which imply $O(n^2)$.