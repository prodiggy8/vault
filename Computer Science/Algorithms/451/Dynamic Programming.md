---
tags:
  - computer-science
  - algorithms
  - course/15-451
type: note
author:
description:
aliases:
date created: Thursday, September 24th 2026, 12:34:45 pm
date modified: Thursday, September 24th 2026, 12:34:49 pm
---
1. Reduce it to numerical problem
2. Define a DP function
3. Set up a recurrence
4. Memoize on bottom up
5. Analyze runtime

### Problem 1: Longest Increasing Subsequence

Given $x_{1}, x_{2}, \dots, x_{n}$, find length of longest strictly-increasing subsequence (not substring so doesn’t need to be contiguous).

1. We restrict the problem to find the size of such sequence
2. Then we define the function `LIS(i) = longest increasing subsequence in A[1..i]`

Example: $[7,0,4,3,10,11,17,5]$ 
`LIS(5) = 3` because the longest subsequence is $[0,3,5]$

3. We set up the recurrence:
$$
\text{LIS}(i)=\begin{cases}
0 & \text{if } i = 0 \\
\max_{\substack{0 \leq j < i \\ a_{j} < a_{i}}}\text{LIS}(j) + 1 & \text{otherwise}
\end{cases}
$$
Answer: $\max_{0 \leq i \leq n}\text{LIS}(i)$ which is $O(n^2)$.

This is very shit so we use a **SegTree** to improve.

We process elements in order like $(\text{val}, \text{idx})$ so $(0,2), (3,4), \dots$

`for all (val, idx): Assign(idx, RangeSum(0, idx) + 1)`

Since it’s sorted we don’t have to worry about the `aj < ai` step anymore and we have an efficient way of doing sums over the subproblems.

- Trace with the example to understand better.
- This is $O(n \log n)$.

### Counting Planar Spanning Trees

Input: $G=(V,E)$, $V=\{0, \dots, n-1\}$.

Vertices at the corner form a convex $n$-gon.
You can also represent  the edges as jumps in a contiguous axis.

`U(i, j) = # of ways to complete i...j that's required to be a tree`
`C(i, j) = # of ways assuming i and j are already connected outside range`

Consider i, j are connected and we dont want to use edges from i to finish up the range i..j
We just do U(i+1, j). 

Now considered not only i is connected to j outside the range, but i is already connected to something in the range i..j, say element k. Then we do C(i, k) and then C(k, j)

$$
C(i,j)=\begin{cases}
1 & \text{if } i + 1 = j \\
U(i+1,j) + \sum_{i<k<j} \delta(i,k)C(i,k)C(k,j) & \text{otherwise}
\end{cases}
$$
Where $\delta$ is the indicator variable of whether $i$ connects to $k$.

$$
U(i,j)=\begin{cases}
\delta(i,j) & \text{if i+1=j} \\
\delta(i,j)C(i,j) + \sum_{i < k < j}\delta(i,k)C(i,k)U(k,j) & \text{otherwise}
\end{cases}
$$

This is $O(n^3)$ because we have two $n^2$ tables to fill and then we need to consider all $k$ on top of it.

### Independent Sets on Trees

Given $G = (V, E)$, an independent set is a subset of vercies such that none of the vertices are adjacent.

max weight IS

w(v)=value of the maximum weight IS of the subtree rooted at v

w(v) = {
$\sum_{u \in C(v)}$ if we dont use v

}