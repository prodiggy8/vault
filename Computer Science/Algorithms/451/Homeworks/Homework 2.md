---
tags:
  - algorithms
type: homework
author:
description:
aliases:
date created: Monday, September 7th 2026, 1:28:14 pm
date modified: Tuesday, September 8th 2026, 6:26:06 pm
---
2a.

Let $B$ be a sorted arrangement of $A$. If $B[i]$ has key $< x$ and $i’<i$ then $\operatorname{key}(B[i’]) \leq \operatorname{key}(B[i]) < x$

We first begin by noting that the elements with key $x$ occupy the indices between $c_x$ and $c_{x+1}-1$. Since there are $c_x$ elements with key less than $x$, they form a segment $0, \dots, c_x - 1$.

A similar argument can show that elements with key $\leq x$ form a segment $0, \dots, c_{x+1}-1$. Since element in index $c_{x+1}$ has key $> x$.

Subtracting the two segments, we get that elements with key $x$ occupy exactly indices $c_x, \dots, c_{x+1}-1$.

Hence, index $j$ is a correct sorted position for key $x$ exactly when $B[j]$ has key $x$, which happens iff $c_x \leq j < c_{x+1}$.

2b.
```pseudo
InplaceCountingSort(A[0..n-1], key):
	B = array of size u
	
	for i from 0 to n - 1:
		B[key(A[i])]++
		
	C = array of size u + 1 initialized to 0
	for i from 0 to u - 1:
		C[i + 1] = C[i] + B[i]
		
	copy(next, C)
	
	for i from 0 to u - 1:
		while next[i] < C[i + 1]:
			j = key(A[next[i]])
			
			if i == j:
				next[i]++
			else:
				swap(A[next[i]], A[next[j]])
				next[j]++	
```

**Complexity**

Until line 11 we perform a constant number of operations on $n$ elements plus some declarations over $u$, so total complexity is $O(n+u)$.

For lines 13-21, the outer loop runs $u$ times. Every time the inner loop runs, we increment either $\operatorname{next}[i]$ or  $\operatorname{next}[j]$. Because the total capacity of all blocks in $\operatorname{next}$ is $n$, the maximum number of times these pointers can be incremented is $n$. Therefore, these last lines sum up $O(n + u)$ and hence, so does the overall algorithm.

For space, we only use three arrays of size bounded by $u$.

**Correctness**

After line 10, it’s clear that $C[x] = c_x$ and $C[x+1] = c_{x+1}$ so elements with key $x$ must be in their range. We define this as an invariant. At each iteration of the while loop, for every $x$: $C[x] \leq \operatorname{next}[x] \leq C[x+1]$ and every element in $A[C[x]..\operatorname{next}[x] - 1]$ has key $x$. Consequently, the number of elements with key $x$ outside $A[c_x..\operatorname{next}[x] - 1]$ is exactly $c_{x+1} - \operatorname{next}[x]$.

Initially this is trivially true since $\operatorname{next} = C$.

For preservation, let $y=\operatorname{key}(A[\operatorname{next[x]}])$ with $\operatorname{next}[x] < c_{x+1}$ by the guard.

- Case $y=x$: the element at slot $\operatorname{next}[x]$ has key $x$, so after the increment the range $A[c_x..\operatorname{next}[x]-1]$ is the old range plus one slot and it still contains only key $x$ elements. Since the guard gives that $\operatorname{next}[x] < c_{x+1}$, after incrementing we have $\operatorname{next}[x] \leq c_{x+1}$.

- Case $y \neq x$: the element at $\operatorname{next}[x]$ is a key $y$ element outside the range $A[c_y..\operatorname{next}[y] - 1]$. By the invariant, $c_{y+1} - \operatorname{next}[y] \geq 1$.