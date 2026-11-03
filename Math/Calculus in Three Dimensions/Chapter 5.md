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


> [!Warning]
> Hard topic, do exercises
> SPECIALLY regarding changing the order of integration


# 5.3 Polar Integrals

We work with **polar rectangles** with sides of size $r$ and $\theta$ and integrate over them.
$$R=\{(r,\theta)| a \leq r \leq b,\alpha \leq \theta \leq \beta\}$$
$$\iint_{R}f(r,\theta)dA = \int_{\alpha}^\beta \int_{a}^b f(r,\theta)\; r \; dr \, d\theta$$

- Remember there’s an extra $r$

**General Region of Integration**

Also has types. It is more common to have $r=f(\theta)$ than otherwise.
$$D=\{(r,\theta)|\alpha \leq \theta \leq \beta, h_{1}(\theta) \leq r \leq h_{2}(\theta)\}$$

> [!Warning]
> Do exercises especially with solids and volumes
> Do one exercise with improper integrals

# 5.4 Triple Integral

- Same story: $\sum_{i=1}^l \sum_{j=1}^m \sum_{k=1}^n f(x^*_{ijk}, y^*_{ijk}, z^*_{ijk}) \Delta x \Delta y \Delta z$
- $\iiint_{B}f(x,y,z)dV = \int_{r}^s \int_{c}^d \int_{a}^b f(x,y,z) dx \; dy \; dz$

**General Region**

We consider a projection of the bounded region of interest onto a plane. 

1. Say the $xy$-plane so that $E=\{(x,y,z)|(x,y) \in D, u\}$
$$
\iiint_{E} f(x,y,z)dV = \iint_{D}\left[\int_{u_{1}(x,y)}^{u_{2}(x,y)} f(x,y,z) dz\right]
$$
# 5.5 Triple Integral in Spherical and Cylindrical

# 5.6 Center of Mass and Moments of Inertia

If object has uniform density, it’s the object’s geometric center.