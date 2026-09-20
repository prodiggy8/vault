---
tags:
  - algorithms
  - computer-science
  - course/15-451
  - amortized-analysis
type: note
author:
description:
aliases:
date created: Saturday, September 19th 2026, 5:12:16 pm
date modified: Saturday, September 19th 2026, 5:25:18 pm
---
Other resources: CLRS, Chapter 17

Amortized analysis applies over a *sequence of operations*

**Dynamic arrays**

- Doubling resizing, distinguish between capacity $c$ and size $n$
- Model: writes and moves cost $1$, all else is free

>[!definition] Aggregate method
>We simply add the **total** cost of performing a sequence of $m$ operations and divide by $m$.

**Theorem:** the amortized cost of append using array doubling is $3$
**Proof:**
- $m$ appends: cost $m$
- The expansions: $1 + 2 + \dots + \frac{\lceil \lceil m \rceil \rceil}{2} \leq 1 + 2 + \dots + m \leq 2m$
- $c=\lceil \lceil m \rceil \rceil$ is the *superceil* of $m$, the smallest power of $2$ less than $m$
- Hence cost is $\frac{3m}{m}=3$
#### Bankers method

>[!definition] Bankers method
>Each operation has a cost and additionally may choose to pay *an extra cost* to store in the data structure for later use. A future operation may use this credit to offset the cost of an expensive operation.

**Theorem:** the amortized cost of append using array doubling is $3$
**Proof:**
- Consider: whenever appending, we pay a credit $2$, total cost $3$
- When resize operation is triggered, the array must be full ($n$ elements). The second half will have each a credit of $2$, hence we have a total of $n$ credits.
- We consume this credit to pay for the cost of moving $n$ elements to the freshly allocated array.

> [!important] Important
> We must never use credit that doesn’t exist, must always argue there’s enough credit.

> [!definition] Potential method
> Consider a sequence of $m$ operations $\sigma_{1}, \dots, \sigma_{m}$ and a sequence of states $S_{0}, S_{1}, \dots, S_{m}$. Operation $\sigma_{i}$ changes state from $S_{i-1}$ to $S_{i}$. Let the actual cost of operation $\sigma_{i}$ in the cost model be $c_{i}$. Given a potential function $\Phi$ we then define the amortized cost **$\text{ac}_{i}$** of $\sigma_{i}$ by:
> $$\text{ac}_{i}=c_{i}+\Phi(S_{i})-\Phi(S_{i-1})$$

The potential function can be thought as a generalization of the credit in the banker’s method. If an operation puts $p$ credit, it’s equivalent to increasing potential by $p$. If it consumes $p$ credits, it’s the equivalent of decreasing potential by $p$. 

In plain English: $\text{amortized cost} = \text{actual cost} + \text{change in potential}$

Summing up the potential formula for a sequence of operations:
$$\sum_{i}\text{ac}_{i}=\sum_{i}(c_{i}+\Phi(S_{i})-\Phi(S_{i-1})=\Phi(S_{m})-\Phi(S_{0})+\sum_{i}c_{i}$$
Rearranging:
$$\sum_{i}c_{i}=\left( \sum_{i} \text{ac}_{i}\right)+\Phi(S_{0})-\Phi(S_{m})$$
>[!theorem] Theorem
>If $\Phi(S_{0})\leq \Phi(S_{m})$:
>$$\sum_{i}c_{i} \leq \sum_{i} \text{ac}_{i}$$

We identify the quantity related to the cost. In this case, the values in the list matter not, just $n$ and $c$. Moreover, it’s the relation between them, that grows when resizing and shrinks when appending.

First attempt: $\Phi(n,c)=n-c$. But this is never positive!

Second attempt: $\Phi(n,c)=n-\frac{c}{2}$. This stems from the fact that when resizing happens, $n=c$. Hence $n \geq \frac{c}{2}$ always.
- Verification with append: $\text{ac}_{i}=1 + \Phi(n + 1, c)-\Phi(n-1, c)=2$
- Verification with resize: 
$$
\begin{align}
\text{ac}_{i}&=n + \Phi(n, 2c) - \Phi(n, c) \\
&=n + n-c -n + \frac{c}{2} \\
&=n-\frac{c}{2} \\
&=\frac{n}{2}
\end{align}
$$
We only decreased the cost of append by a factor of $\frac{n}{2}$! We weren’t able to offset the cost. From this, we have an easy third candidate: $\Phi(n,c)=2\left( n-\frac{c}{2} \right)$.
- Verification with append: $\text{ac}_{i}=1 + \Phi(n + 1, c)-\Phi(n, c)=3$
- Verification with resize:
$$
\begin{align}
\text{ac}_{i}&=n + \Phi(n, 2c) - \Phi(n, c) \\
&=n + 2n-2c -2n + c \\
&=n-c \\
&=0
\end{align}
$$
**We’re done!**

#### Shrinking

We define `pop()` and shrinking. Erasing costs $1$.
We shrink if $n=\frac{c}{4}$ and $c \geq 4$.

**Analysis**

$\frac{c}{2}$ is still the center. When $n=\frac{c}{2}$ means we either just resized the array, either to grow or shrink. So it would be nice if the potential was $0$ at these points. We start with the same function from before.

Notice that unlike growing, shrinking only needs $\frac{n}{4}$ pops to happen and then we only copy $\frac{n}{4}$ elements anyway! That means only $1$ token in the bankers method would be necessary.

We define:
$$
\Phi(n,c)=
\begin{cases}
2\left( n-\frac{c}{2} \right) & \text{if } n \geq \frac{c}{2} \\
\frac{c}{2} -n & \text{if } n < \frac{c}{2}
\end{cases}
$$
**Proof:**
Consider the cost of pop. Erasing an element costs $1$. We consider each case. First when $n \geq \frac{c}{2}$, potential goes down by 2.
$$\Phi(n-1, c) - \Phi(n,c) = 2(n-1) - c - 2n + c=-2$$
Now when $n <\frac{c}{2}$, potential goes up by 1.
$$\Phi(n-1, c ) - \Phi(n,c)=\frac{c}{2}-n+1-\frac{c}{2} + n=1$$
Hence potential is at most 1 and amortized cost is 2. Notice that this function is continuous, so when $n=\frac{c}{2}$ and $\Phi(n-1,c)=\frac{c}{2}-n$ while $\Phi(n,c)=2\left( n-\frac{c}{2} \right)$ we have 0 in both sides so we don’t consider that case separately.

Now shrink. Before shrink occurs $c=4n$ and hence the initial potential is $n$ (by $\Phi$) which is exactly the cost of moving the $n$ elements to the new array. Hence the amortized cost of shrink is 0.

Now considering the sequence of $m$ operations: $\Phi(S_{0})=1, \Phi(S_{m})\geq 0$ so we do not satisfy the criteria. However we can just account for this $1$ as the cost of initialization and we get our desired property $\Phi(S_{0}) \leq \Phi(S_{m})$.

#### Problem 13
Describe the difference between amortized analysis using the aggregate method and average case analysis. How are they different? What about *expected* cost analysis? Where does this fit in and how is it different then the first two?

Amortized analysis considers a sequence of $m$ operations and we average over them. We guarantee a sequence of $m$ operations has that cost.

Average case analysis fixes a probability distribution over the input and calculates expectation. We don’t guarantee anything, just claim worse cases are unlikely.

Expected cost analysis considers worst case input and then we calculate the expectation of the randomness inside our algorithm.

#### Problem 14

Give a proof of the following theorem using the banker’s method.

>[!theorem] Theorem
>Using the doubling-halving array the amortized cost of append is at most 3 and the amortized cost of pop is at most 2 and the amortized cost of initialization is at most 1.

We already proved the top half of the theorem above. Now we move on to pop. Consider that shrinking happens when $n=\frac{c}{4}$.

If $n\leq\frac{c}{2}$ we assign one credit per pop. Hence amortized pop costs 2.
If $n > \frac{c}{2}$ we **use** two credits per pop. Hence amortized pop costs 1t and empties the credit store.

Consider that a resizing just happened and assume our credit is 0. After $m$ appends we have $2m$ credits. Pop consumes two credits since $n + m > \frac{c}{2}$ hence after $m$ pops we go back to 0.

Now consider we pop with $n\leq \frac{c}{2}$. Each pop gives us one credit. If $n \leq \frac{n}{4}$ we have $\frac{n}{4}$ credits and use them to move the elements to the new $\frac{n}{2}$ sized array.