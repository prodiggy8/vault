---
tags:
  - algorithms
  - computer-science
  - course/15-451
type: note
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Monday, September 7th 2026, 1:32:14 pm
date modified: Monday, September 7th 2026, 1:32:24 pm
---
## Word RAM model

- We have unlimited registers each storing a $w$-bit word
- Reading, writing, arithmetic, and logic operations on a **constant** number of words is free
- With input size $n$, we need $w \geq \log n$

For the last assumption: otherwise we wouldn’t be able to write $n$ as an index.

Example: multiplying $n$ integers, each $w$ bits long. The result would occupy $nw$ bits, that is, $n$ registers. We can only multiply a constant number of words in constant time, so this would take much more than $O(n)$.

Example: search with free preprocessing. In comparison model, we get $\Omega(\log n)$. In integer model, we get $O(1)$. For integers $a_1, \dots, a_n$ in range $\{0, 1, \dots, u - 1\}$ where $u \leq 2^w$, we create an array $T$ of size $u$ and place $T[a_i] = i$, that is, we create a lookup table of indexes, indexed by the values.

## Sorting

Given $a_1, \dots, a_n$, each identified by a not necessarily unique $key(a_i)$. 
Must output $a_{\pi_{1}}, \dots, a_{\pi_{n}}$ such that $key(a_{\pi_{1}}) \leq \dots \leq a_{\pi_{n}}$.

- For distinct keys in range $\{1, \dots, n\}$
We create an array $A$ of size $n$ and place $A[key(a_i)]=a_i$.

- For distinct keys in range $\{0, \dots, u - 1\}$ with $u \leq 2^w$
We create an array $A$ of size $u$, place $A[key(a_i)]=a_i$ and filter out the empty slots.

 - For possibly repeated keys in range $\{0, \dots, u - 1\}$ with $u \leq 2^w$

```pseudo
CountingSort(A[1..n], key):
	L = array of u empty lists
	for each x in a:
		Append x to L[key(x)]
		
	M = empty list
	for each l from 0 to u - 1:
		M.extend(L[l])
	
	return M
```

Runs in $O(n+u)$ since we make one pass over input of size $n$ then one pass over $u$ possible keys. It is stable since it appends elements in order to the lists.

If $u \in O(n)$ then this is better than comparison sort, i.e., if integers have $O(\log n)$ bits.

### Tuple Sorting

Given $n$ elements where each element’s key is a tuple $(k_1, k_2, \dots, k_d)$, we want to sort by key.