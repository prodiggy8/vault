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


3.  a)

```
StreakSort(A[1..n]):
	Let B be an empty sequence
	start = 1
	
	for i from 1 to n-1:
		if A[i+1] < A[i]:
			Append A[start..i] to B
			start = i+1
	
	Append A[start..n] to B
	
	while |B| > 1:
		Let B' be an empty sequence
		j = 0
		while j <= |B|:
			if j + 1 <= |B|:
				Append Merge(B[j], B[j+1]) to B'
			else:
				Append B[j] to B'
			j += 2
		B = B'
		
	return B[1]
```

**Correctness**

Lines 2-11:

The scan cuts the array exactly at the positions $i$ where $A[i+1] < A[i]$. Let $m$ be the number of streaks it produces. Between two consecutive cuts every adjacent pair satisfies $A[i] < A[i+1]$, so each streak $B_j$ is strictly increasing. Conversely, any valid partition into $t$ streaks must cut at every such "descent" position, so the streaks we produce are the maximal increasing runs. In particular $m \leq t$, since a partition into $t$ streaks has $t − 1$ cuts and each of our $m − 1$ descents must be one of them.

Lines 12-23:

Assuming every sequence in $B$ is increasing and the collection 


3. b)

Fix any $t$. We’ll proceed by finding an input made of $t$ streaks on which the algorithm must make at least $c \cdot (n + n \log t)$ comparisons. We handle $t=1$ and $t \geq 2$ separately, since $t=1$ implies the target is just $n$ and when $t\geq 2$ we have $n \leq n \log t$, so $n + n\log t \leq 2n\log t$.

Case $t=1$

Feed the algorithm the array $1, 2, \dots, n$. Suppose it finishes in fewer than $n-3$ comparisons. Then there’s some neighboring pair of positions $i$ and $i+1$ (with $2 \leq i \leq n-2$) that it never compared directly.

Now suppose a second array, the same one, but with values at $i$ and $i+1$ swapped. Every comparison the algorithm made gives the exact same answer on this new array. That’s because no direct comparison was made, and a comparison between either element with some other arbitrary $q$ will yield the same result, because $q$ is either smaller or greater than both (by the fact they’re adjacent).

However, since the second array is a valid input (with streaks $(1, \dots, i+1$) and $(i, \dots, n)$) and the two arrays are different orderings of the same numbers, they need different rearrangements to sort them. Hence, the algorithm must make at least $\Omega(n)$ comparisons.

Case $t \geq 2$

Assume $t | n$ and let $m=\frac{n}{t}$. View the array as a $t \times m$ grid, Column 1 gets the values $1..t$, column 2 gets $t+1..2t$, and so on. Within each column, you can order those $t$ values top-to-bottom however you like, independently per column. Two things are true about any array built this way:

- Each row is increasing, because everything in column $j$ is smaller than everything in column $j+1$.
- Each row is its own streak: the last entry of a row is from the last column, so it’s big. The first entry of the new row is from column 1, so it’s at most $t$.

So every array has exactly $t$ streaks, each of length $m \geq 2$, and is a legal input. Each column has $t!$ possible orderings, and the $m$ columns are chosen independently, so $t!^m$ arrays. They’re all different orderings of the numbers $1..n$, so each needs a different sorting rearrangement. By the lecture’s rule, the algorithm needs at least $m \cdot \log_{2}(t!)$ comparisons.

Finally, a bound on $t!$: pair up the factors of $(t!)^2$ as $1\cdot t,\; 2\cdot(t-1),\; 3\cdot(t-2),\;\ldots,\; t\cdot 1$, i.e.
$$(t!)^2 = \prod_{k=1}^{t} k\,(t+1-k).$$
Each pair multiplies to at least $t$, since
$$k(t+1-k) - t = (k-1)(t-k) \ge 0 \quad\text{for } 1 \le k \le t.$$
There are $t$ pairs, so $(t!)^2 \ge t^t$, i.e. $t! \ge t^{t/2}$. Plugging in:
$$\ell \;\ge\; m \log_2(t!) \;\ge\; m \cdot \frac{t}{2}\log_2 t \;=\; \frac{n}{t}\cdot\frac{t}{2}\log_2 t \;=\; \frac{n}{2}\log_2 t \;\ge\; \frac{1}{4}\bigl(n + n\log_2 t\bigr).$$
Hence, for $t=1$ at least some input needs $n$ comparisons, and for $t \geq 2$ some input needs at least a quarter of $n+n \log t$.

Edge case: if $t$ doesn’t divide $n$, then use $\left\lfloor  \frac{n}{t}  \right \rfloor$ columns and tackle the leftover values onto the end in increasing order. For $t=1$ with $n < 4$, the bound is trivial.
