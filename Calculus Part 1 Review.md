---
tags:
  - calculus
type:
author:
description:
aliases:
date created: Sunday, October 18th 2026, 5:19:52 pm
date modified: Sunday, October 18th 2026, 5:19:58 pm
---
# 2.3
$$
u \cdot v = |u||v| \cos \theta
$$
If **orthogonal**: $u \cdot v = 0$
If **parallel**:
$$
\begin{align}
u &= cv \\
u \cdot v &= \pm|u||v|
\end{align}
$$
### Projections
$$\operatorname{proj}_{u}v=\frac{u \cdot v}{|u|^2} \hat{u}$$
Is the component of $v$ in the **direction of $u$**

Example of use:
- Want to change basis of $u$ to be $v$ and $w$ such that $v \perp w$
$$u=\operatorname{proj}_{v}u + \operatorname{proj}_{w}u$$
- Suppose we only have one vector $v$ and need to find $w$
$$u = \operatorname{proj}_{v}u + (u - \operatorname{proj}_{v}u)$$

# 2.4

$$u \times v = \langle u_{2}v_{3} - u_{3}v_{2}, u_{3}v_{1} - v_{3}u_{1}, u_{1}v_{2} - u_{2}v_{1} \rangle $$
The result is orthogonal to both.

- Anticommutative: $u \times v = -(v \times u)$
- i -> j -> k
	- Clockwise product: positive direction
	- Counterclockwise: negative direction
- Scalar triple product: $u \cdot (u \times w) = (u \times v) \cdot w$
- $|u \times v| = |u||v| \sin \theta$

There’s matrix method, parallelogram, and triangle areas left.

# 2.5

$$
\langle x,y,z \rangle=\langle x_{0}, y_{0}, z_{0} \rangle + t \langle a,b,c \rangle
$$
$$
\begin{align}
x=x_{0} +ta && y=y_{0}+tb && z=z_{0}+tc
\end{align}
$$
$$\frac{x-x_{0}}{a} = \frac{y-y_{0}}{b}=\frac{z-z_{0}}{c}$$

Finding from two points: direction vector $\overrightarrow{PQ}=Q - P$ and initial point $P$.

#### Distance between a point and a line

Want to distance from line $L$ closest to $M$.

1. Pick arbitrary point in line $P$
2. $d=\frac{|\overrightarrow{PM} \times v|}{|v|}$

#### Plane

Given by three points that do not lie on the same line.

- Normal is parallel to the plane.
- $n \cdot \overrightarrow{PQ} = 0$
- 
