---
tags:
type:
author:
description:
aliases:
date created: Wednesday, September 23rd 2026, 2:17:50 pm
date modified: Wednesday, September 23rd 2026, 2:17:52 pm
---
# Almost Palindrome

Let t be a substring of $s$ with length m. We compare pairs $(0, m-1)$ then $(1, m-2)$ and so on.
Let $(l,r)$ be the **first** mismatch if there is one (\*)

**Claim:** If deleting any character gives a palindrome, then deleting $l$ or $r$ suffices.
*Proof:* Suppose we delete $k$ and the result $u$ is a palindrome (\*\*).

- **Case $k<l$**:
Pick a $q \in \left[ k, l-1 \right]$.
1. By (\*\*) $t[q+1] = t[m - q - 1]$.
2. By (\*) $t[q] = t[m-q-1]$ too.
3. Hence it must be that $t[q]=t[q+1]$
A similar argument can be made for every character in the range $\left[k, l-1\right]$. The range is all equal characters. If they’re equal, then deleting $t[l]$ works the same as deleting $t[k]$.

- **Case $k>r$**
The argument above is symmetric.

- **Case $l < k < r$**
In this case $u[l]=u[r] \implies t[l]=t[r]$, which contradicts (\*).

Hence we can describe a palindrome as:
- $S=i+j$ with $i,j$ being the endpoints of $t$, i.e., $S$ is twice the midpoint of $t$
- The first mismatch $(l,r)$
- An inner palindrome: either $t[l+1, r]$ or $t[l, r-1]$.


## Manacher’s algorithm

First a trivial one:
```pseudo
p = empty array
for i = 1; i <= n; i++:
	while (s[i - p[i]] == s[i + p[i]]):
		p[i]++ 
```

Palindromic strings can be odd or even. Manacher simplifies that:
- Insert “#” between characters
	- abba becomes \#a\#b\#b\#a\#, i.e., every string becomes n’=2n + 1
- Sentinels @original word$ to handle boundaries safely

Keep $l$ and $r$ representing the boundaries of the **rightmost** palindrome found so far
Start from index 1 end before n - 1
```c++
for (int i = 1; i <= n; i++) {
	int mirror = l + r - i // mirror of i around center (l + r)/2
	
	// if i lies inside rightmost palindrome
	// if palindrome of radius p[mirror] sits at mirror
	// the mirrored copy of its sits at i as long as within bounds
	if (i < r)
		// r - i is how far you can go from i before hitting the right edge
		p[i] = min(r-i, p[mirror])
	
}
```

___

`T = s[i..j]`

Suppose deleting `s[p]` turns `T` into a palindrome.
`q = i + j - p` is the mirror of `p` about the center and suppose `p <= c`

Claim: deleting `s[p]` turns `T` into a palindrome iff `S[p+1, q]` 





# Problem 2

**Preprocessing:** 
- Let keys be stored in array $A$
- We create an array $B$ of size $n+m$ such that:
	- $B[0..m-1]=0$ and $B[m..n + m - 1] = 1$
- We create a hash map $H$ such that $H[A[i]] = m + i$

This is all $O(n+m)$.

**Data Structure:**
- We create a segment tree with two auxiliary variables:
	- The hash map $H$
	- A variable $\text{front} = m$
- Then the operations become:

```pseudo
Find(x):
	return H(x)
	
Move(x):
	front--
	Assign(H(x), 0)
	Assign(front, x)
	H[x] = front
```

The complexity of find is $O(1)$ and the complexity of move is $O(\log(n+m))$ as we have an $n+m$ sized SegTree.