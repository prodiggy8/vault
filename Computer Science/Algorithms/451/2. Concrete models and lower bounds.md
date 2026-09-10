---
tags:
  - algorithms
  - course/15-451
  - computer-science
type: note
author:
  - Gustavo Grancieiro
description: Concrete models and lower bounds
aliases:
date created: Tuesday, September 1st 2026, 12:33:19 pm
date modified: Monday, September 7th 2026, 12:47:42 pm
---
> [!definition] Upper bound
> There exists an algorithm that for every input of length $n$ costs at most $U_n$

> [!definition] Lower bound
> For any algorithm, there exists an input of length $n$ that costs at least $L_n$

There is no formal definition of “all algorithms” hence we go by models.

> [!definition] Comparison Model
> An algorithm may compare two elements at a cost of 1. Moving the elements, copying, swapping is *free*. No other operations on the items are allowed (using them as indices, adding them, hashing them).
> 
> Also called **decision tree** model. Each node is a comparison.

### Adversary Techniques

Example: trying to prove that $n-1$ comparisons are needed to find a maximum. If we say “because we need to compare all elements”, that could be done in mere $\frac{n}{2}$ comparisons.

Proof: Suppose $a_i$ and $a_j$ who never lost a comparison, with $a_i > a_j$. If the algorithm outputs $a_j$ it’s incorrect. Else we can construct another input that is the same except $a_j > a_i$. On the new input, the results of the comparisons are the same, so the answer must still be $a_i$, which would wrong. Therefore, there must be $n-1$ elements that lose a comparison.

This is the type of proof we did with **pancakes in 251**. We argue that if an algorithm that made too few we can come up with an input that makes it produce the wrong answer.

### Decision Trees

We must argue some property about the structure of **any possible decision tree** for the problem. The worst case will be the **longest root-to-leaf path**.

Proof: At the root node there of any decision tree for this problem there are $n$ possible outputs. For each comparison, exactly one element loses, and hence the set of outputs is one fewer than at parent node. Therefore all decision trees have depth $n-1$.

==**Remark:**== $[c, a, b, d]$ and $[b, d, a, c]$ sort to **different** permutations $[a_2, a_3, a_1, a_4]$ and $[a_3, a_1, a_4, a_2]$ while $[c, a, b, d]$ and $[m, d, e, z]$ sort to the **same** $[a_2, a_3, a_1, a_4]$. The comparison model doesn’t know values, only sequence of comparisons.

### Information Theory

There are $n!$ different input sequences. We assume elements are distinct so every input has a **unique** output, hence $n!$ outputs. If the algorithm makes $c$ comparisons whose results are encoded by a sequence of binary outcomes $b_1, b_2, \dots, b_n$, the algorithm can produce $2^c$ outputs. Hence at least $\log n!$ comparisons are needed.

$$2^c \geq n! \implies c \geq \log n!$$

This argument is generalizable: **any algorithm that needs to produce $M$ outputs needs $\log M$ comparisons**. Also:

$$\log n! = \log n + \log n-1 + \dots + \log 1 < n \cdot \log n \in O(n \log n)$$

$$\log n!=\log n + \log n-1 + \dots + \log 1 > \frac{n}{2}\log \frac{n}{2} \in \Omega(n \log n)$$

In the comparison model, **binary insertion sort** is $O(n \log n)$ too!

#### When the number of inputs is not clear

Sorting with $n$ elements, with at most $1 \leq D \leq n$ distinct elements. We already know an upper bound for the case $D=n$. We now want a lower bound for **all** $D$.

Technique: we focus on a **subset** of the inputs! How to choose?
- Needs to have a lot of outputs
- Needs to be simple enough to count

Proof: Take $\frac{n}{D}$ independently shuffled permutations of $1 \dots D$ concatenated. Since they are unique (all permutation sort to the same values, but must go through different comparisons), 
no one output can correctly sort two of these inputs. Then, we must count how many inputs:
$$(D!)^{\frac{n}{D}}$$
By the generalizable argument above, we need these many comparisons:
$$\log\left( (D!)^{\frac{n}{D}} \right)=\frac{n}{D}\log D! = \frac{n}{D} \Theta(D \log D)=\Theta(n \log D)$$

- [ ] Do exercises from [Erickson’s](https://jeffe.cs.illinois.edu/teaching/algorithms/notes/12-lowerbounds.pdf)
- [ ] Do exercises from notes
- [ ] Do exercises from recitation

