
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

Proof: At the root node there




