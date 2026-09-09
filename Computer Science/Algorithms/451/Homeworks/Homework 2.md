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
#### 1a)

$$T(n) = \lceil \frac{64}{\log_{b} 2} \rceil (n + b) = \lceil \frac{64}{\log_{b} 2} \rceil (10^6 + b)$$
Ignoring the ceiling and constants, we minimize $f(b) = \frac{(n+b)}{\ln b}$
$$f'(b) = \frac{\ln b - (n+b)/b}{(\ln b)^2} = 0 \iff b(\ln b - 1) = n.$$
Solving numerically in Python gives $b^* \approx 10^5$ so each digit carries $\log_2 10^5 \approx 16.6$ bits, so the 64 bits are consumed in $\lceil 64/16.6 \rceil = 4$ passes, and the total cost is $T(b^*) = 4\,(n + b^*) \approx 4.4 \times 10^6$ operations.

#### 1b)

A family $H$ of 4 functions is universal iff each of the $28$ pairs $x \neq y$ collides under at most $4/2 = 2$ of its functions. After brute forcing:

| $x$   | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- |
| $h_1$ | 0   | 0   | 0   | 0   | 1   | 1   | 1   | 1   |
| $h_2$ | 0   | 0   | 1   | 1   | 0   | 0   | 1   | 1   |
| $h_3$ | 0   | 1   | 0   | 1   | 0   | 1   | 0   | 1   |
| $h_4$ | 0   | 1   | 1   | 0   | 1   | 0   | 0   | 1   |

Each row of the table has a simple description. Write $x$ with three binary digits, $x = (x_2 x_1 x_0)$, so for example $5 = 101$. Then $h_1(x) = x_2$ is the leftmost digit (it is $1$ exactly for $x = 4, 5, 6, 7$), $h_2(x) = x_1$ is the middle digit ($1$ for $x = 2, 3, 6, 7$), $h_3(x) = x_0$ is the rightmost digit ($1$ for odd $x$), and $h_4(x) = x_0 \oplus x_1 \oplus x_2$ is $1$ exactly when $x$ has an odd number of $1$ digits ($x = 1, 2, 4, 7$).

Take any $x \neq y$ and count. The first three functions read off the digits of $x$, so $h_1, h_2, h_3$ send $x$ and $y$ to the same location exactly as often as $x$ and $y$ have the same digit in a position. The fourth function compares how many $1$ digits they have, and this parity is the same exactly when they differ in an even number of positions. Since $x \neq y$, they differ in $1$, $2$ or $3$ positions:
- differ in $1$ position: they agree on $2$ digits, and their parities differ, so $2$ collisions.
- differ in $2$ positions: they agree on $1$ digit, and their parities agree, so $1 + 1 = 2$ collisions.
- differ in $3$ positions: they agree on no digit, and their parities differ, so $0$ collisions. 
In every case at most $2$ of the $4$ functions send $x$ and $y$ to the same location, so $\Pr_{h \in H}[h(x) = h(y)] \leq 2/4 = 1/2$, and $H$ is universal.

#### 1c)

Not universal. 

A family $H$ is universal if for all distinct keys $x \neq y$, $\Pr_{h \in H}[h(x) = h(y)] \leq 1/m$; here $m = 2$ and $|H| = 5$, so each pair may collide under at most $2$ of the $5$ functions. Take $x = b$, $y = d$: $g(b) = g(d) = 1$, $i(b) = i(d) = 1$ and $j(b) = j(d) = 0$, so $$\Pr_{h \in H}[h(b) = h(d)] = \frac{3}{5} > \frac{1}{2}.$$
#### 2a)

Let $B$ be a sorted arrangement of $A$. If $B[i]$ has key $< x$ and $i’<i$ then $\operatorname{key}(B[i’]) \leq \operatorname{key}(B[i]) < x$

We first begin by noting that the elements with key $x$ occupy the indices between $c_x$ and $c_{x+1}-1$. Since there are $c_x$ elements with key less than $x$, they form a segment $0, \dots, c_x - 1$.

A similar argument can show that elements with key $\leq x$ form a segment $0, \dots, c_{x+1}-1$. Since element in index $c_{x+1}$ has key $> x$.

Subtracting the two segments, we get that elements with key $x$ occupy exactly indices $c_x, \dots, c_{x+1}-1$.

Hence, index $j$ is a correct sorted position for key $x$ exactly when $B[j]$ has key $x$, which happens iff $c_x \leq j < c_{x+1}$.

#### 2b)

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

- Case $y \neq x$: the element at $\operatorname{next}[x]$ is a key $y$ element outside the range $A[c_y..\operatorname{next}[y] - 1]$. By the invariant, $c_{y+1} - \operatorname{next}[y] \geq 1$. So $\operatorname{next}[y] < c_{y+1}$, i.e. slot $\operatorname{next}[y]$ lies in block $y$ but outside $A[c_y..\operatorname{next}[y]-1]$. Slots $\operatorname{next}[x]$ and $\operatorname{next}[y]$ lie in different blocks and outside their settled ranges, so the swap touches no settled range. After it, $A[\operatorname{next}[y]]$ has key $y$, so incrementing $\operatorname{next}[y]$ extends $A[c_y..\operatorname{next}[y]-1]$ by one slot of key $y$, and $\operatorname{next}[y] \leq c_{y+1}$ since it was strictly less before. Nothing else changes, so the invariant holds.

For termination, each iteration increments exactly one entry of $\operatorname{next}$, so $\sum_x (c_{x+1} - \operatorname{next}[x])$ decreases by one per iteration. By the invariant this quantity is $\geq 0$, and initially $= n$, so the inner loop runs at most $n$ times in total.

When the while loop for $x$ exits, $\operatorname{next}[x] \geq c_{x+1}$ by the guard, hence $\operatorname{next}[x] = c_{x+1}$ by the invariant. Entries of $\operatorname{next}$ never decrease, so this remains true.

After the outer loop, $\operatorname{next}[x] = c_{x+1}$ for all $x$, so by the invariant $A[c_x..c_{x+1}-1]$ contains only key-$x$ elements. Since $c_0 = 0$, $c_u = n$ and $c$ is non-decreasing, these blocks partition $A[0..n-1]$ in increasing key order, so $A$ is sorted by key. As we only ever swap, $A$ is a permutation of the input.

#### 3a)

Fix distinct keys $x,y,z\in U$ and targets $v_1,v_2,v_3$ we show $\Pr_{h\in\mathcal H}[h(x)=v_1\wedge h(y)=v_2\wedge h(z)=v_3]=\frac{1}{m^3}$.

Think of $R$ as $cm$ independent uniform $b$-bit cells. A key $k$ reads one cell per column, its cells $C(k)=\{(k_i,i):0\le i<c\}$, and $h(k)=\bigoplus_{e\in C(k)}R[e]$. Two keys read the same cell in column $i$ exactly when they agree on chunk $i$, so a column that separates two keys is one where they read different, hence independent, cells: a cell in $C(x)\setminus C(y)$ is fresh randomness entirely independent of $h(y)$, because $h(y)$ is a function of the cells in $C(y)$ alone. This is the mechanism from the recitation. We define a lemma:

**Lemma.** Let $k$ be a key, $T$ a set of other keys, and suppose some cell $e\in C(k)$ is read by no key in $T$. Then for all $v$ and all targets $(v_t)_{t\in T}$
$$\Pr[h(k)=v \wedge \forall t \in T : h(t) = v_{t}]=\frac1m \Pr[\forall t \in T : h(t) = v_{t}].$$

Proof: Fix the values of all cells other than $e$. No key in $T$ reads $e$, so under this fixing each $h(t)$, $t\in T$, is a constant and $E_T=\{\forall t\in T:\ h(t)=v_t\}$ either holds or fails and $h(k)=a\oplus R[e]$ with $a$ constant. Since $R[e]$ is uniform on $\{0,1\}^b$ and independent of the fixed cells, Lemma 1 of recitation says $a\oplus R[e]$ is uniformly random, so under this fixing $\Pr[h(k)=v]=1/m$ for every $v$. Thus for every fixing, the conditional probability of $h(k)=v\wedge E_T$ is $1/m$ if $E_T$ holds under that fixing and $0$ otherwise. By the law of total probability over the fixings, $$\Pr[h(k)=v\wedge E_T]=\tfrac1m\Pr[E_T]$$ With $T=\emptyset$ this says every single $h(k)$ is uniform.

The lemma lets us isolate one key at a time.

**Claim.** Among any three distinct keys, some key has a cell that neither of the other two reads.

*Proof.* If some column $i^{\ast}$ separates all three ($x_{i^{\ast}},y_{i^{\ast}},z_{i^{\ast}}$ pairwise distinct), then $(x_{i^{\ast}},i^{\ast})$ is read by $x$ alone. Otherwise pick a column $i_1$ with $x_{i_1}\ne y_{i_1}$; since $i_1$ does not separate all three, $z_{i_1}$ equals exactly one of $x_{i_1},y_{i_1}$. If $z_{i_1}=y_{i_1}$ then $(x_{i_1},i_1)$ is read by $x$ alone; if $z_{i_1}=x_{i_1}$ then $(y_{i_1},i_1)$ is read by $y$ alone. So any column where the keys don't all agree has an odd one out, and the odd one out reads a cell nobody else touches.


Proof of 3-wise independence. By the claim, one of the three keys has a cell that neither of the other two reads. Nothing in the statement distinguishes the three keys (each comes with its own target), so we may name that key $x$ and the cell $e_1$. Now apply the lemma three times. First take $k=x$ and $T=\{y,z\}$ with the cell $e_1$: this pulls $h(x)=v_1$ out of the event at a cost of a factor $1/m$, leaving $h(y)=v_2\wedge h(z)=v_3$. Next, since $y\ne z$, they differ in some chunk $i_2$, so the cell $(y_{i_2},i_2)$ is read by $y$ and not by $z$; take $k=y$ and $T=\{z\}$ with that cell. This pulls out $h(y)=v_2$ at another factor $1/m$. Finally take $k=z$ and $T=\emptyset$: $h(z)$ by itself is uniform, giving the last factor $1/m$. 
$$
\begin{aligned}
\Pr[h(x)=v_1\wedge h(y)=v_2\wedge h(z)=v_3] &=\tfrac1m\,\Pr[h(y)=v_2\wedge h(z)=v_3]\\ &=\tfrac1{m^2}\,\Pr[h(z)=v_3]\\ &=\tfrac1{m^3}
\end{aligned}
$$

Each factor is the conditional probability of the key holding the private cell, and the last key is uniform on its own. So $H$ is 3wise independent.

#### 3b)

We show $H$ is not four-wise independent when $c\ge 2$. (If $c=1$ then $h(x)=R[x][0]$ is a uniformly random function of the key, which is $k$-wise independent for every $k$). Take the four keys that differ only in their first two chunks and are $0$ everywhere else:
$$
\begin{aligned}
x=\langle 0,0,0,\dots,0\rangle \\
y=\langle 0,1,0,\dots,0\rangle \\
z=\langle 1,0,0,\dots,0\rangle \\
u=\langle 1,1,0,\dots,0\rangle.
\end{aligned}
$$
In column $0$, $x$ and $y$ read $R[0][0]$ while $z$ and $u$ read $R[1][0]$; in column $1$, $x$ and $z$ read $R[0][1]$ while $y$ and $u$ read $R[1][1]$; in every column $i\ge 2$ all four keys read $R[0][i]$. Let $r=\bigoplus_{i=2}^{c-1}R[0][i]$ be the XOR of those shared cells:
$$\begin{aligned} h(x)&=R[0][0]\oplus R[0][1]\oplus r, & h(y)&=R[0][0]\oplus R[1][1]\oplus r,\\ h(z)&=R[1][0]\oplus R[0][1]\oplus r, & h(u)&=R[1][0]\oplus R[1][1]\oplus r. \end{aligned}$$
Each of the four cells $R[0][0],R[1][0],R[0][1],R[1][1]$ appears in exactly two of these, and $r$ in all four, so XORing the four values cancels everything:
$$h(x)\oplus h(y)\oplus h(z)\oplus h(u)=0$$
$h(u)=h(x)\oplus h(y)\oplus h(z)$ is determined by the other three hash values, whatever the table. Now choose the targets $v_1=v_2=v_3=0$ and $v_4=1$. Four-wise independence needs $h(x)=0\wedge h(y)=0\wedge h(z)=0\wedge h(u)=1$ to have probability $1/m^4>0$. But on that event the identity gives $0\oplus 0\oplus 0\oplus 1=0$, so the event is empty. Hence $H$ is not four-wise independent.