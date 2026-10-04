---
tags:
  - algorithms
  - splay-trees
  - course/15-451
  - computer-science
type: nore
author:
  - Gustavo Grancieiro Ramalho
description:
aliases:
date created: Tuesday, September 22nd 2026, 11:12:10 pm
date modified: Tuesday, September 22nd 2026, 11:12:14 pm
---
**Key idea:** whenever we access a node, move it to the root

### Splaying
Is the operation that moves a node to the root in $O(\log n)$ time amortized.

##### Zig rule
We’re moving $x$ and its parent $y$ is the **root**. 
Rotate $x$ about $y$.

##### Zig-zag rule
We’re moving $x$ with parent $y$ and grandparent $z$.
**$x$ and $y$ are not both left or right children**.
Rotate $x$ about $y$.
Rotate $x$ about $z$.

##### Zig-zig rule
We’re moving $x$ with parent $y$ and grandparent $z$.
**$x$ and $y$ are both left or right children**.
**Rotate $y$ about $z$**
**Rotate $x$ about $y$**

Search: must splay right after it
Split: splay the node you want to split, remove right subtree
Join: splay rightmost node of $A$ and attach $B$ to the right

### Analysis
Assume each node $x$ has a weight $w$. We can choose the weight assignment that gives the best bound, i.e., we give elements that are frequently accessed a higher weight.

Size of node: $s(x)=\sum_{y \in T(x)}w(y)$
Rank of node: $r(x)=\lfloor \log s(x) \rfloor$

Define $\Phi(T) = \sum_{x \in T} r(x)$

1. Doing a rotation between a pair of nodes only affect the two nodes! 
2. If $y$ is $x$’s parent, then rank of $y$ before the rotation is the rank of $x$ after the rotation.

### Access Lemma
Suppose we splay $T$ to get $T’$
$$\text{amortized splaying steps} = \text{actual splaying steps} + \Phi(T') - \Phi(T) \leq 3(r(t)-r(x)) + 1$$
##### Auxiliary lemmas

> [!lemma] Rank rule
> If two siblings have the same rank $r$, then the parent has rank $\geq r + 1$.

Conversely: if parent and sibling have rank $r$ then $x$ must have rank $<r$

> [!lemma] Cost of one splay step
> Zig-zig or zig-zag step costs:  
> $$
> 3(r(z)-r(x))
> $$
> Zig step costs:
> $$
> 3(r(y)-r(x))+1
> $$

Notice we can say that $r(z)$ is really $r'(x)$ which is the rank of $x$ after the rotation. Via telescopic sum:
$$
\begin{align}
3(r'(x) - r(x)) \\
3(r''(x) - r'(x)) \\
\dots \\
3(r(t) - r(x))
\end{align}
$$

##### Zig Case
Actual cost is $1$.
$r'(x) = r(y)$ since $x$ is now the root.
Since $y$ used to be the root its rank can’t increase, so $r'(y) \leq r(y)$. 
Hence the difference in potential is at most:
$$(r(y) + r(y)) - (r(x) + r(y))=r(y) - r(x)$$
$$ \text{amortized cost} = (r(y) - r(x))+1 \leq 3(r(y)-r(x))+1$$
##### Zig-zag Case
We split into two cases:

**Case 1:** The rank does not increase between the starting node and the ending node of the step, i.e., $r(z) \leq r(y) \leq r(x)$.

Since the rank of child can’t be greater than the rank of a parent, $r(z)=r(y)=r(x)$ in this case.

We know $r'(x) = r(z)$. Hence, by the rank rule, either $r'(y)$ or $r’(z)$ are $<r'(x)=r(z)$. Hence the potential has decreased by at least one after the splay. Hence:
$$\text{amortized}=\text{cost} + \Delta \Phi \leq 1 + (-1) = 0$$
This fits the bound we’re trying to prove: $0 \leq 3(r(z) - r(x))$.

**Case 2:** The rank does increase, i.e., $r(x) < r(z)$.

First, we know $r'(x) = r(z)$.

Notice that after the splay $y$ and $z$ have only a fraction of their previous descendants, so $r'(y) \leq r(y)$ and $r'(z) \leq r(z)$. 
$$
\begin{align}
\Delta \Phi&= r'(z) + r'(y) + r'(x) - r(z) - r(y) - r(x) \\
&\leq r(z) + r(y) + r(z) - r(z) - r(y) - r(x) \\
&\leq 2r(z) - r(z) - r(x) \\
&\leq 2r(z) - (r(x) + 1) - r(x) && \text{by fact } r(x) < r(z) \\
&\leq 2(r(z) - r(x)) - 1
\end{align}
$$
Adding the actual cost of $1$ we get $2(r(z) - r(x)) \leq 3(r(z) - r(x))$, our bound.
##### Zig-zig Case

**Case 1:** The rank does not increase, i.e., $r(z) = r(y) = r(x)$.

For the intermediate state (after rotating $y$ about $z$), $y$ is the new root, hence $r'(y) = r(z)$. Since $x$’s descendants don’t change $r'(x) = r(x) = r(z)$. Hence by the rank rule it must be that $r'(z) < r(z)$. Looking at the final tree, $z$’s descendants also don’t change, hence $r''(z) < r(z)$.

Hence the potential decreases by at least $1$ and gives us amortized cost of $0 \leq 3(r(z)-r(x))$.

**Case 2:** The rank does increase, i.e., $r(x) < r(z)$.

Notice $y$ and $z$ are going to end up being children of $x$, hence $r'(z) \leq r(x) = r(z)$ and $r(y)\leq r(z)$. Also $r(y) \geq r(x)$ since it’s an ancestor of $x$ at the beginning.
$$
\begin{align}
\Delta \Phi&=r'(z)+r'(y)+r'(x)-r(z)-r(y)-r(x) \\
&\leq r(z) + r(z) + r(z) - r(z) - r(y) - r(x) \\
&\leq 3r(z) - (r(x) + 1) - r(x) - r(x) & \text{By fact } r(x) < r(z) \\
&=3(r(z)-r(x)) - 1
\end{align}
$$
Which cancels out with the actual cost.

## Balance Theorem

A sequence of $m$ splays in a tree of $n$ nodes takes $O(m \log n + n \log n)$.

*Proof.*

Suppose all weights equal $1$.

$$\begin{align}
\text{actual number of splaying steps}  + (\Phi(T')-\Phi(T)) \leq 3(\log n - \log |T(x)|) + 1
\end{align}$$