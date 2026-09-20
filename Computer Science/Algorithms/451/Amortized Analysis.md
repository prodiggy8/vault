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

The potential function can be thought as a generalization of the credit in the banker’s method.


