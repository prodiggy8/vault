---
tags:
type:
author:
description:
aliases:
date created: Thursday, September 24th 2026, 11:20:12 am
date modified: Thursday, September 24th 2026, 12:19:11 pm
---
# Intuition

A pseudo-palindrome is a palindrome with an extra character wedged in. A pseudo-palindrome is going to be symmetric until we reach this character then it becomes out of step by 1, but the piece inside it is still a palindrome.

So a pseudo-palindrome is two palindromic layers with their axes of symmetry half a position apart:
- an inner one symmetric about $c$
- an outer one symmetric about $c\pm \frac{1}{2}$
- the one character that shifts the axis.
We just search for these three things.

Let $s=[0..L-1]$ be a palindrome and let $i$ be the first mismatch from the outside, i.e., $s[i] \neq s[L-1-i]$.

**Lemma 1:** If deleting some character gives a palindrome then deleting the ends gives a palindrome.

*Proof.*

Say the deletion is at position $k$ and the result is a palindrome.

- $k$ inside the mismatched pair ($i < k < L-1-i$). Then $s[i] \neq s[L-1-i]$ is still a mismatched pair. It can’t be a palindrome.
- $k<i$.
	- By the fact the result is palindrome: $s[k+1]=s[L-1-k-1]$
	- By the fact $i$ is the first mismatch: $s[k]=s[L-1-k]$
	- Hence $s[k]=s[k+1]$. A similar argument can be made for every element $j$ such that $k \leq j \leq i$. Since it’s a sequence of equal characters, deleting $i$ would also work.

Hence a pseudo-palindrome is a string of the form $T[a-1-i..b+1]$ where $T[a..b]$ is a palindrome with $b \geq a$, $T[a-1] \neq T[b]$, and $T[a-1-j]=T[b+j]$ for all $j \leq i$.

#### The algorithm

Let $T[a..b]$ be the substring of length $\rho$ centered at $c$ (so $\rho = b − a + 1$). Let $P(c)$ be the length of the longest palindrome centered at $c$. We call $\rho$ _eligible_ if $1 \leq ρ \leq P(c)$ and $T[a−1] ≠ T[b]$.

**Claim:** For a fixed $(c,\text{side})$, the best candidate uses the largest eligible $\rho$.

That’s because $\rho'$ candidate is contained in $T[a..b]$ (the inner palindrome of $\rho$), and $\rho$'s candidate strictly contains $T[a−1..b]$.

So for every $(c, \text{side})$:

1. $P(c)$: we can use Manacher’s algorithm to do this in $O(n)$. If anybody asks us how to prove Manacher’s complexity, then we do a binary search on the length for each $c$ in $O(n \log n)$.

2. The largest eligible $\rho$
	- Start at the pair for $\rho=P(c)$ and walk inward until the first mismatch $T[a-1] \neq T[b]$. For $k$ steps we know $T[a-1..a-2+k]=T[b-k+1..b]$ so we just do binary search on $k$ again in $O(n \log n)$.
	- The largest eligible $\rho$ will be $P(c)-2k$.

3. The extension $i$: the largest $i$ with $T[a-1-i..a-2]$ equal to the reverse of $T[b+1..b+i]$, capped by the ends of $T$. Binary search once more in $O(n \log n)$.

Output the maximum of $\rho + 1 + 2i$ over all $(c, \text{side})$. 

**Correctness:**


#### Queries

We are comparing strings all the time! For all of the above to work in $O(n \log n)$ we need to be able to do so in $O(1)$. We want $\frac{1}{n}$ failure overall. We are going to run $O(n \log n)$ tests so we pick $k=n^3 \log n$ and select a random prime from $[2, 2k\log k]$. Prime selection is crazy cheap compared to anything else done here.

Run prefix hashes of both the string and it’s reverse in $O(n)$ and we now have constant-time comparisons. 

The total probability of error is (by union-bound) $\frac{Qn}{k}=\frac{1}{n}$.

#### Complexity

A prime at most $O(n^3 \log n)$ still fits in size $\log n$. Since the input has $n$ cells we have $w \geq \log n$ so it fits in $O(1)$ space and so does every operation $\mod p$. Prime selection runs in $\text{poly}(n)$ and will be dominated by the rest. Hence we’re left with the binary searches on expansions which give us $O(n \log n)$.



