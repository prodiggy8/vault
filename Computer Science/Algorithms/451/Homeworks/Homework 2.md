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

- To be done


3a)
Fix distinct keys $x,y,z\in U$ and targets $v_1,v_2,v_3$ we show $\Pr_{h\in\mathcal H}[h(x)=v_1\wedge h(y)=v_2\wedge h(z)=v_3]=\frac{1}{m^3}$.

Think of $R$ as $cm$ independent uniform $b$-bit cells. A key $k$ reads one cell per column, its cells $C(k)=\{(k_i,i):0\le i<c\}$, and $h(k)=\bigoplus_{e\in C(k)}R[e]$. Two keys read the same cell in column $i$ exactly when they agree on chunk $i$, so a column that separates two keys is one where they read different, hence independent, cells: a cell in $C(x)\setminus C(y)$ is fresh randomness entirely independent of $h(y)$, because $h(y)$ is a function of the cells in $C(y)$ alone.

This is the mechanism of Recitation 2 where the column $A_i$ appears in $h(y)$ but not in $h(x)$, and Method 2 fixes all other columns and applies the chain rule. We define a lemma:

**Lemma.** Let $k$ be a key, $T$ a set of other keys, and suppose some cell $e\in C(k)$ is read by no key in $T$. Then for all $v$ and all targets $(v_t)_{t\in T}$, writing $E_T=\{\forall t\in T:\ h(t)=v_t\}$,
$$\Pr[h(k)=v\wedge E_T]=\tfrac1m\Pr[E_T].$$

*Proof.* Fix the values of every cell except $e$; call the assignment $\rho$. No key in $T$ reads $e$, so under $\rho$ each $h(t)$ is a constant and whether $E_T$ holds is decided by $\rho$. Meanwhile $h(k)=a_\rho\oplus R[e]$ with $a_\rho$ constant, and $R[e]$ is uniform and independent of $\rho$, so by Lemma 1 of recitation $\Pr[h(k)=v\mid\rho]=\Pr[R[e]=a_\rho\oplus v]=1/m$ for every $\rho$. Averaging over $\rho$,
$$\Pr[h(k)=v\wedge E_T]=\sum_{\rho:\,E_T\text{ holds}}\Pr[\rho]\cdot\tfrac1m=\tfrac1m\Pr[E_T].\qquad\blacksquare$$
With $T=\emptyset$ this says every single $h(k)$ is uniform.

The lemma lets us peel keys off one at a time, so the question becomes combinatorial. Peeling $y$ from $z$ is free: $y\ne z$ differ in some chunk $i_2$, so $(y_{i_2},i_2)\in C(y)\setminus C(z)$. The real work is the first peel, which is the hint's case analysis.

**Claim.** Among any three distinct keys, some key has a cell that neither of the other two reads.

*Proof.* If some column $i^{\ast}$ separates all three ($x_{i^{\ast}},y_{i^{\ast}},z_{i^{\ast}}$ pairwise distinct), then $(x_{i^{\ast}},i^{\ast})$ is read by $x$ alone. Otherwise pick a column $i_1$ with $x_{i_1}\ne y_{i_1}$; since $i_1$ does not separate all three, $z_{i_1}$ equals exactly one of $x_{i_1},y_{i_1}$. If $z_{i_1}=y_{i_1}$ then $(x_{i_1},i_1)$ is read by $x$ alone; if $z_{i_1}=x_{i_1}$ then $(y_{i_1},i_1)$ is read by $y$ alone. In words: any column where the keys don't all agree has an odd one out, and the odd one out reads a cell nobody else touches. $\blacksquare$

*Proof of 3-wise independence.* The statement is symmetric in the pairs $(x,v_1),(y,v_2),(z,v_3)$, so by the Claim we may relabel so that $x$ has a cell $e_1\notin C(y)\cup C(z)$. Apply the Lemma three times, with $(k,T)=(x,\{y,z\})$ using $e_1$, then $(y,\{z\})$ using $(y_{i_2},i_2)$, then $(z,\emptyset)$:
$$\Pr[h(x)=v_1\wedge h(y)=v_2\wedge h(z)=v_3]=\tfrac1m\Pr[h(y)=v_2\wedge h(z)=v_3]=\tfrac1{m^2}\Pr[h(z)=v_3]=\tfrac1{m^3}.\qquad\blacksquare$$
This is Method 2's chain rule: each factor is the conditional probability of the key holding the private cell, and the last key is uniform on its own, playing the role of the offset $c$.

The only place "three" was used is the Claim, and it fails for four keys (see part (b)).