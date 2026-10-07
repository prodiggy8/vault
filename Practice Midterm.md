---
tags:
type:
author:
description:
aliases:
date created: Wednesday, October 7th 2026, 10:10:22 am
date modified: Wednesday, October 7th 2026, 10:10:24 am
---
Dynamic median

$0$ to $u-1$

Add(x) -> add x to the list
FindMedian() -> return median

RangeSum
Assign(i, x)

Log u time per call


1. NumAtMost(x)

For each element i in list, we create an array where A\[i\] = 1 and 0 otherwise.
We create a SegTree on such array.
Then, NumAtMost(x) = RangeSum(0, x)
By lecture, RangeSum takes O(log u) so NumAtMost takes O(log u) as well.

2. FindMedian in O(log^2 u)

We run binary search on NumAtMost(x) until we find x such that NumAtMost(x) = u/2.

# Tree Labeling

Tree of n nodes

Leaves are labeled with numbers (1..B)

Goal: label the rest of the nodes with numbers from the same set minimizing TOTAL DEVIATION of the tree.

Deviation: sum over all edges (x,y) of |label(x) - label(y)|

$f(x, l)=$ min total deviation for tree rooted at x if x has label l

If x is a leaf:
0 if has label l and is a leaf
inf if doesnt have label l and is a leaft
else:

$$\sum_{v \in T(x)} \min_{0 \leq l' \leq B} |l - l'| + f(v, l')$$

min 0 <= l <= B f(v, l)