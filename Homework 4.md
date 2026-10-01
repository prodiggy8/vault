---
tags:
type:
author:
description:
aliases:
date created: Tuesday, September 29th 2026, 8:19:30 pm
date modified: Tuesday, September 29th 2026, 8:19:35 pm
---
# Problem 1

1. 
$$\Phi(\langle x,y \rangle )=3x$$

2. 
$$\Phi(\langle x,y \rangle )=2|x-y|$$
3. 
$$\Phi(\langle x, y, z \rangle )=2x+y$$

## Problem 2

Let $P[0] = 0$ and $P[i] = a_1 + \dots + a_i$, computed in $O(n)$ time. The block $a_j, \dots, a_i$ then has sum $S(j,i) = P[i] - P[j-1]$, available in $O(1)$.

**Subproblems:** For $1 \le j \le i \le n$, let $L[j][i]$ be the maximum length of a strictly increasing summed array of the prefix $a_1, \dots, a_i$ whose last block is exactly $a_j, \dots, a_i$, or $-\infty$ if no such array exists. We define the recurrence:

$$
\begin{align}
L[1][i] &= 1 \\
L[j][i] &= 1 + \max\{\, L[k][j-1] : 1 \le k \le j-1,\ S(k, j-1) < S(j, i) \,\} \qquad (j \ge 2)
\end{align}
$$

where the max of an empty set is $-\infty$ and $1 + (-\infty) = -\infty$.

$L[j][i]$ depends only on entries with right endpoint $j - 1 < i$, so we fill the table in increasing order of $i$.

For the final answer, we just do $\max_{1 \le j \le n} L[j][n]$. Every summed array of $a$ has some last block $a_j, \dots, a_n$, so this covers all cases. It is at least $L[1][n] = 1$ (the whole array as one block).

**Correctness**

*Case $j = 1$.* The last block is the entire prefix $a_1, \dots, a_i$, so it is the only block and the length is 1.

*Case $j \ge 2$.* The last block does not start at $a_1$, so there is a previous block. It ends at $a_{j-1}$, so it is $a_k, \dots, a_{j-1}$ for some $1 \le k \le j-1$.

- ($\le$) Take any valid array for $(j, i)$. Removing its last block leaves a strictly increasing summed array of $a_1, \dots, a_{j-1}$ with last block $a_k, \dots, a_{j-1}$, so it has length at most $L[k][j-1]$. Since the original array is strictly increasing, $S(k, j-1) < S(j, i)$. Hence the original length is at most $1 + L[k][j-1]$, which is at most the right-hand side of the recurrence.
- ($\ge$) Take any $k$ with $S(k, j-1) < S(j, i)$ and $L[k][j-1] > -\infty$, and append the block $a_j, \dots, a_i$ to an optimal array for $(k, j-1)$. The result is a summed array of $a_1, \dots, a_i$ with last block $a_j, \dots, a_i$. It is strictly increasing because the old blocks already were, and the only new pair of consecutive blocks satisfies $S(k, j-1) < S(j, i)$. Hence $L[j][i] \ge 1 + L[k][j-1]$ for every such $k$.
- If no such $k$ exists, no valid array for $(j, i)$ exists, which matches the empty max giving $-\infty$.

**Complexity**

There are $O(n^2)$ subproblems. Each takes a max over $O(n)$ values of $k$, and each $k$ is checked in $O(1)$ using prefix sums. With the $O(n)$ prefix-sum computation, the total is $O(n^3)$.

# Problem 3

## a)
We create a union-find structure that will be used to keep track of vertices that can’t be separated by removing an edge, with both path compression and union-by-size. We add a variable to the structure keeping the number of sets. The representative element of each set is the element with smallest depth in the set. We also keep the original spanning tree to track parents and (pre-computed) depth of each node. All of this is $O(n)$.

## b)
`AddRoads(u, v)` will do the following:
- Go up in the tree with two pointers starting at the sets of `u` and `v` until they meet. At each step we take the pointer whose set has the deeper top `t` and do `Union(t, parent(t))`, which moves that pointer to the set on the other side of the tree edge `(t, parent(t))` and decreases the number of sets by one.

`NumBridges()` just returns the value of the variable for number of sets we set in the beginning in $O(1)$.

**Correctness:**
- Notice that by definition an edge $(u,v)$ is not a bridge if there is another path from $u$ to $v$ that does not include such edge. Hence there is a cycle containing edge $(u,v)$ and every edge in this cycle is not a bridge.
- When adding an edge to the spanning tree, we create a cycle and hence destroy bridges. Such cycle contains the edge we added and the tree path between its endpoints.
- Invariant: the sets of the union-find are exactly the groups of vertices that cannot be separated by removing a single edge, and each set is a connected subtree of the spanning tree with its stored `top` being its shallowest node. Initially every node is its own set, which holds since in a tree any two vertices are separated by cutting the path between them.
- Given the invariant, contracting each set into a single node leaves a tree whose edges are exactly the bridges: edges inside a set are on a cycle, edges between sets disconnect the graph when removed. A tree on $s$ nodes has $s − 1$ edges, so `NumBridges()` correctly returns (number of sets − 1), initially $n − 1$.
- By traversing the tree we merge exactly the sets on the path from $u$ to $v$. The set containing the lowest common ancestor of $u$ and $v$ has a top at least as shallow as the lowest common ancestor, while any other set on the path is strictly below the lowest common ancestor and has a strictly deeper top. So the pointer we advance is never the one at the lower common ancestor's set, the edge `(t, parent(t))` is on the path, and the pointers meet at the lowest common ancestor’s set without overshooting. Each `Union(t, parent(t))` merges two distinct sets, since `parent(t)` is shallower than `t` and hence outside `t`'s set, and the merged set is again a connected subtree whose top is the shallower of the two tops, so the invariant is preserved. Sets off the path are never touched.
- Hence if the path contains k edges that are still bridges, we perform exactly k unions and the number of sets decreases by exactly k, matching the k bridges destroyed.
- We prove amortized complexity together with part c.

## c)
- We already know by lecture (CLRS proof) that any sequence of $m$ `Find`/`Union` operations on a union-find with path compression and union-by-size runs in $O(m \cdot \alpha(n))$ total.
- It remains to count the operations our traversal performs over $m$ calls to `AddRoads`. Every iteration of the loop does `Union(t, parent(t))`, which by correctness merges two distinct sets. The structure starts with $n$ sets and never has fewer than one, so over the entire sequence of $m$ insertions the loop runs at most $n − 1$ times in total.
- Each iteration performs a constant number of union-find operations: two `Find`s for the meeting test, one comparison of top depths, one `Find` of `parent(t)`, and one `Union`. Each call to `AddRoads` additionally performs the two `Find`s of its final, failing meeting test. So the total number of union-find operations is at most $c₁(n − 1) + c₂ m = O(n + m)$. 
- Applying the theorem with $m = O(n + m)$, the $m$ insertions run in $O((n + m) \cdot \alpha(n))$ total.
- Amortized cost: dividing the total by the number of operations, each of the $n$ initializations and $m$ insertions costs $O(\alpha(n))$ amortized. A single `AddRoads` can still take $O(n \cdot \alpha(n))$, but it does so by spending unions from the shared budget of $n − 1$, which no later call can spend again.
