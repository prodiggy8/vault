---
tags:
  - algorithms
  - course/15-451
  - union-find
type:
author:
description:
aliases:
date created: Tuesday, September 22nd 2026, 12:30:57 pm
date modified: Tuesday, September 22nd 2026, 6:35:22 pm
---

> [!warning] Recall
> Kruskal: sort edges by weight and scan. Add to current forest if $(u, v)$ are not already connected. Takes $O(|E| \log |E|)$.

## Union-Find Problem

Disjoint sets

We use a representative element to identify it

`MakeSet(x)` creates new set with $x$

`Find(x)` find representative element of set containing $x$

`Union(x, y)` forms a new set that is the union of sets containing $x$ and $y$

**Kruskal:** we `MakeSet(u)` $\forall u (u \in G)$. For each $(u,v)$ we find the set of $u$ and the set of $v$. If they are not the same, we union. We’ll make $|V|$ sets, perform $|V|-1$ unions and $2|E|$ finds.

### How to implement?

1. We maintain a set representative manually: $O(n)$ union and $O(1)$ find.
2. Graph with adjacency list: $O(1)$ union and $O(n)$ find.
3. **Tree** with root as representative: $O(1)$ union and $O(n)$ find.
	- We can improve the tree model to be faster.
#### Optimizing union

It’s dangerous to create very unbalanced trees. 

We define a size function and use it to make the **smaller tree the child of the larger tree**. We get $O(\log n)$ find this way.

**Why?** Every edge is created by a union-by-size. Whenever we move from a node to its parent, the total size of the tree rooted at the current node **at least doubles**. Since any tree has at most $n$ elements, find costs at most $O(\log n)$.

#### Optimizing find with path compression

Idea: whenever we do a find, we change the **parent of every node visited to point directly to the roo**t so future finds don’t travel as much.

```pseudo
Find(x): 
	if p(x) != x: 
		p(x) = Find(p(x))
	return p(x)
```

Where `p(x)` is the direct parent of `x`. We recurse up until we find the root and point all elements on the way to it. It will cost **the number of elements it touches.** The cost of link will be $1 + \log n$ and the cost of find $2 + \log n$.

##### Proof

> [!definition] Heavy and light nodes
> 1. **heavy** if $\operatorname{size}(u)>\frac{1}{2}\operatorname{size}(p(u))$
> 2. **light** otherwise

> [!lemma] Light lemma
> Any root-to-leaf path has **at most** $\log n$ **light nodes**. By definition, since we at least halve the size of tree rooted at current every edge.

We can’t say much about the amount of heavy nodes, but we can say each node can have at most **one heavy children** by definition. When we compress a node, another might become heavy. But this can only happen a certain number of times. A node $u$ with $\operatorname{size}(u)$ can only be halved $\log(\operatorname{size}(u))$ times. Hence:

$$\Phi(F)=\sum_{u \in F}\log(\operatorname{size}(u))$$

1. The potential is initially $0$ and always positive
2. Increases when union is done
3. Decreases when find is done

- **MakeSet** creates one node, $\log(1)=0$, hence no change in potential and amortized cost $1$.$\operatorname{size}(x)$ is at least $1$ hence $\log(\operatorname{size}(x)) \geq 0$
- **Link**. Suppose we attach $y$ to $x$.
	- $\operatorname{size}(x) \geq 1 \implies \log(\operatorname{size}(x)) \geq 0$
	- $\operatorname{size'}(x) \leq n \implies \log(\operatorname{size'}(x)) \leq \log n$
	- $\Delta \Phi = \Phi' - \Phi=\log(\operatorname{size'}(x))-\log(\operatorname{size}(x)) \leq \log n$
	- Hence cost is at most $1 + \log n$
- **Find.** 

![[Union-Find.png]]

By looking at the picture we notice all nodes except first and last have their size decreased, while the others stay the same. So size can only ever decrease and  so does potential.

On find’s path: $1 + \text{\#heavy} + \text{\#light}=1 + \text{\#heavy} + \log n$

# Problems

17. Consider union-find with path compression. We perform $n$ MakeSet operations, followed by $m$ unions then $f$ finds in that order. Show the total cost of this sequence is $O(n+m+f)$, i.e., each operation takes constant amortized time. (Hint: define potential function that is the degree of the root of the tree).

We define:
$$\Phi(F)=\sum_{u \in F, \: p(u)=u} \deg(u)$$
where $\deg(u)$ is the number of direct children of $u$.

MakeSet: $\operatorname{ac}=1+\Delta \Phi=1$ since MakeSet only ever creates roots, not children. Hence, the total cost is $n$.

18. 


