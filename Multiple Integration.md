---
tags:
  - calculus
type:
author:
description:
aliases:
date created: Monday, October 19th 2026, 12:00:08 pm
date modified: Monday, October 19th 2026, 12:00:20 pm
---
# 5.1 Double Integrals Rectangular

We consider a rectangular region $R = \{(x,y) \in R^2 | a \leq x \leq b, c \leq y \leq d\}$ and surface $z=f(x,y)$.

###### Double Riemann Sum

$$V \approx \sum_{i=1}^m \sum_{j=1}^n f(x^*_{ij},y^*_{ij})\Delta A$$
Such that $\Delta x=\frac{b-a}{m}$, $\Delta y=\frac{d-c}{n}$, and $\Delta A=\Delta x \Delta y$.
$x^*_{ij}$ and $y^*_{ij}$ are arbitrary sample points in each sub region.

###### Double Integral

$$\iint_{R} f(x,y) dA$$

Property: if $m \leq f(x,y) \leq M$, then:
$$
m \cdot A(R) \leq \iint_{R}f(x,y)dA \leq M \cdot A(R)
$$

**Area of $R$** given by $A(R)=\iint_{1}dA$

Property: if we can separate $f(x,y)=g(x)h(y)$ then:
$$\iint f(x,y)dA=\left( \int_{a}^b g(x)dx \right)\left( \int_{c}^d h(y)dy \right)$$

**Fubini’s Theorem**: integrating with respect to $x$ first or $y$ first yields the same result.

**Average:** $\frac{1}{A(R)}\iint f(x,y)dA$

# 5.2 Double Integrals General

Arbitrary region $D$ inside rectangle $R$. Define $g(x,y) = \begin{cases} f(x,y) & \text{ if } (x,y) \in D \\ 0 & \text{otherwise} \end{cases}$
#### Type I

Two vertical lines for $x$, two functions $g_{1}(x)$ and $g_{2}(x)$ for $y$.
$$D=\{(x,y) | a \leq x \leq b, g_{1}(x) \leq y \leq g_{2}(x)\}$$
$$\iint_{D}f(x,y)dA=\int_{a}^b\left[ \int_{g_{1}(x)}^{g_{2}(x)}f(x,y)dy\right]dx$$
#### Type II

Two horizontal lines for $y$, two functions $h_{1}(y)$ and $h_{2}(y)$ for $x$.
$$D=\{(x,y)|h_{1}(y) \leq x \leq h_{2}(y), c \leq y \leq d\}$$
$$\iint_{D}f(x,y)dA=\int_{c}^d \left[ \int_{h_{1}(y)}^{h_{2}(y)}f(x,y)dx\right]dy$$
> [!important]
> Integrate with respect to the lines first, dependent variable becomes the inner integral.

#### Decomposing

Sometimes it’s useful to divide $D$ into a type I and a type II non-overlapping regions.





# 5.3 Polar Integrals
We work with a **polar rectangle** instead of Cartesian ones to define the sum.
$$R=\{(r,\theta) | a \leq r \leq b, \alpha \leq \theta \leq \beta\}$$
# 5.4 Triple Integrals


