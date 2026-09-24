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

#### How to describe a palindrome?

Let t be a substring of $s$ with length m. We compare pairs $(0, m-1)$ then $(1, m-2)$ and so on.
Let $(l,r)$ be the **first** mismatch if there is one (\*)

**Lemma 1:** If deleting any character gives a palindrome, then deleting $l$ or $r$ suffices.
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

#### How to pick the right pair $l, r$ to delete?

Fix $S$ and without loss of generality with delete $l$. 

Let $x,y$ be the maximal palindrome with center sum $S+1$. Manacher’s algorithm computes these in $O(n)$ for every center. The inner palindrome in $s[l+1,r]$ must be contained in it.
# Problem 1



# Problem 2

**Preprocessing:** 
- We create an array $B$ of size $n+m$ such that:
	- $B[0..m-1]=0$ and $B[m..n + m - 1] = 1$
- We build an array $\text{pos}[x]=m+x$ keeping track of the leaf each key lives
- We build a SegTree of size $n+m$ based on $B$

This is all $O(n+m)$.

**Data Structure:**
- We define two auxiliary variables within the SegTree:
	- A variable $\text{front} = m$
	- The array $\text{pos}$
- Then the operations become:

```pseudo
Find(x):
	return RangeSum(0, pos[x])
	
Move(x):
	front--
	Assign(pos[x], 0)
	Assign(front, 1)
	pos[x] = front
```

The complexity of both find and move is $O(\log(n+m))$ as we have an $2(n+m) - 1$ sized SegTree.

# Problem 3a

Give every red item weight $\frac{1}{n}$ and every blue item weight $\frac{1}{m}$. The total weight is $n \cdot \frac{1}{n} + m \cdot \frac{1}{m}=2$ so the root has $s(t)=2$ and $r(t)=1$.

Take a red item $x$. Its subtree contains $x$ so $s(x) \geq \frac{1}{n}$ and $r(x) \geq \log\left( \frac{1}{n} \right) = -\log n$. By the Access Lemma, the amortized number of splay steps is:

$$3(r(t) - r(x)) + 1 \leq 3(1 + \log n) + 1 = 4 + 3 \log n$$
For a blue item, $s(y) \geq \frac{1}{m}$ gives $r(y) \geq -\log m$ and the same computation yields $4 + 3\log m$.

This is explained by the fact weights exist only in the analysis, the two bounds hold at once for every way of coloring items red and blue. What the bound really says is about the sequences of operations. If you keep hitting a small set of items, the cost of hauling them is paid once. The algorithm doesn’t need to know the colors, it adapts to the access pattern.

# Problem 3b

With unit weights, $r(\text{root})=\lfloor \log 10^6 \rfloor=19$ 