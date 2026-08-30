---
tags:
type:
author:
description:
aliases:
date created: Sunday, August 30th 2026, 12:59:02 pm
date modified: Sunday, August 30th 2026, 12:59:05 pm
---
### Probability

A random variable $X$ assigns a number to each outcome.
$$
\mathbb{E}[X]=\sum_{x} x \cdot Pr[X=x]
$$
**Linearity of Expectation**
$$
\mathbb{E}[X + Y] = \mathbb{E}[X] + \mathbb{E}[Y]
$$
$$
\mathbb{E}[cX]=c \cdot \mathbb{E}[X]
$$
Always! Even if the variables are dependent.

**Indicator Variables**
$$
I_{A}=1 \text{ when event } A \text{ happens and } 0 \text{ otherwise}
$$

**Independence**
$Pr(A \cap B) = Pr(A) \cdot Pr(B)$
$Pr(A|B) = Pr(A)$

**Rules**
$Pr(A \cup B) = Pr(A) + Pr(B)$ for disjoint sets 
$Pr(E) = 1 - Pr(\overline{E})$
$Pr(A \cap B) = Pr(A) \cdot Pr(B | A)$ regardless of independence

*Law of Total Probability* as follows from chain and partition rules
Given event $E$ and a partition, $Pr(E) = Pr(S_1) \cdot Pr(E | S_{1}) + \dots$


