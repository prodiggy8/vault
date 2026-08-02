---
tags:
  - algorithms
type:
author:
description:
aliases:
date created: Sunday, August 2nd 2026, 7:46:48 pm
date modified: Sunday, August 2nd 2026, 7:46:52 pm
---
```pseudo
MergeSort(A[1..n]):
	if n > 1:
		m = floor(n/2)
		MergeSort(A[1..m])
		MergeSort(A[m..n])
		Merge(A[1..n], m)
		
Merge(A[1..n], m):
	i = 0
	j = m + 1
	
	for k in [1..n]:
		if j > n:
			B[k] = A[i]
			i++
		else if i > m:
			B[k] = A[j]
			j++
		else if A[i] < A[j]:
			B[k] = A[i]
			i++
		else:
			B[k] = A[j]
			k++
		
	for k in [1..n]:
		A[k] = B[k]
```

### Complexity
$$
\begin{gather}
T(n)=2T( \frac{n}{2}) +T_{merge}(n) \\
T(n)=2T(\frac{n}{2}) + O(n) \\
T(n) \in O(n \log n)
\end{gather}
$$