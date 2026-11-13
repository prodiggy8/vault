---
tags:
type:
author:
description:
aliases:
date created: Thursday, November 12th 2026, 7:56:33 pm
date modified: Thursday, November 12th 2026, 7:56:37 pm
---
### Problem 1

By the chain rule:
$$\frac{\partial x}{\partial s} = x_u u_s + x_v v_s, \qquad \frac{\partial x}{\partial t} = x_u u_t + x_v v_t,$$
and similarly for $y$. In matrix form:
$$\begin{pmatrix} x_s & x_t \\ y_s & y_t \end{pmatrix} = \begin{pmatrix} x_u & x_v \\ y_u & y_v \end{pmatrix} \begin{pmatrix} u_s & u_t \\ v_s & v_t \end{pmatrix}$$
Since $\det(AB) = \det A \cdot \det B$:
$$\frac{\partial(x,y)}{\partial(s,t)} = \frac{\partial(x,y)}{\partial(u,v)} \cdot \frac{\partial(u,v)}{\partial(s,t)}$$
### Problem 2
By triangle inequality we want the largest to be less than sum of other two. We try to find the complement, which is when either:
$$
\begin{align}
U_{1} \geq U_{2} + U_{3} \\
U_{2} \geq U_{1} + U_{3} \\
U_{3} \geq U_{1} + U_{2}
\end{align}
$$
Only one can happen at once and by symmetry they’re equally likely, so we only need to calculate one. 
$$\begin{aligned} P(U_1\ge U_2+U_3) &=\int_0^1\int_0^{1-u_2}\int_{u_2+u_3}^1 du_1\,du_3\,du_2 \\ &=\int_0^1\int_0^{1-u_2}(1-u_2-u_3)\,du_3\,du_2 \\ &=\frac12\int_0^1(1-u_2)^2\,du_2 =\frac16 \end{aligned}$$
So the probability is $3 \cdot \frac{1}{6}=\frac{1}{2}$.

### Problem 3

- Two cylinders
For a fixed $x\in[-1,1]$, $y$ and $z$ range from $-\sqrt{1-x^2}$ to $\sqrt{1-x^2}$. The cross-section is a square of area
$$A(x)=\left(2\sqrt{1-x^2}\right)^2=4(1-x^2).$$
$$V_2=\int_{-1}^1 4(1-x^2)\,dx =4\left[x-\frac{x^3}{3}\right]_{-1}^1 =\frac{16}{3}.$$
- Three cylinders
$$x^2+y^2\le1,\qquad x^2+z^2\le1,\qquad y^2+z^2\le1.$$
The region has identical octants. In the first, the portions where $x$, $y$, or $z$ is the largest coordinate have equal volumes, since the equations are unchanged by exchanging coordinates. We compute the volume in the first octant where $x$ is largest coordinate then multiply by $8 \cdot 3 = 24$. The conditions become:
$$
0\le y,z\le x,\qquad
y,z\le\sqrt{1-x^2}
$$
Thus the cross-section is a square with side length $m(x)=\min(x,\sqrt{1-x^2})$.

To check the third cylinder, the largest value of $y^2+z^2$ occurs at the corner $(m(x),m(x))$. The smaller bound switches at $x=1/\sqrt2$:
- If $0\le x\le1/\sqrt2$, the side length is $x$, so the square's area is $x^2$. Since $y,z\le x$, we have $y^2+z^2\le2x^2\le1$.
- If $1/\sqrt2\le x\le1$, the side length is $\sqrt{1-x^2}$, so the square's area is $1-x^2$. Since $y,z\le\sqrt{1-x^2}$, we have $y^2+z^2\le2(1-x^2)\le1$.

Thus the third cylinder removes nothing from either square. At $x=1/\sqrt2$, both area formulas give $1/2$. Integrating:

$$ \begin{aligned} V_3 &=24\left[ \int_0^{1/\sqrt2}x^2\,dx +\int_{1/\sqrt2}^1(1-x^2)\,dx \right] \\ &=24\left[ \left[\frac{x^3}{3}\right]_0^{1/\sqrt2} +\left[x-\frac{x^3}{3}\right]_{1/\sqrt2}^1 \right] \\ &=24\left[ \frac1{6\sqrt2}+\frac23-\frac5{6\sqrt2} \right] \\ &=8(2-\sqrt2) \end{aligned} $$

### Problem 4
At height $z$, the sphere has a circular cross-section of radius $\sqrt{R^2-z^2}$ and area $\pi(R^2-z^2)$. The cap extends from $z=R-h$ to $z=R$, so
$$ V=\pi\int_{R-h}^{R}(R^2-z^2)\,dz$$
Set $t=R-z$:
$$ \begin{aligned} V &=\pi\int_0^h\left(R^2-(R-t)^2\right)\,dt \\ &=\pi\int_0^h(2Rt-t^2)\,dt \\ &=\pi\left[Rt^2-\frac{t^3}{3}\right]_0^h. \end{aligned}$$
Hence:
$$V=\pi h^2\left(R-\frac h3\right)$$
When $h=R$,

$$V=\frac23\pi R^3 =\frac12\left(\frac43\pi R^3\right)$$
which is half the volume of the sphere

### Problem 5
##### a)
For $0 \le xy < 1$:

$$\frac{1}{1-xy} = \sum_{n=0}^\infty (xy)^n$$
All terms are nonnegative, so we can do term by term integration.
$$\begin{aligned}\int_0^1\int_0^1 \frac{1}{1-xy}dx\,dy &=\sum_{n=0}^{\infty}\int_0^1\int_0^1x^ny^n\,dx\,dy \\ &=\sum_{n=0}^{\infty} \left(\int_0^1x^n\,dx\right) \left(\int_0^1y^n\,dy\right) \\ &=\sum_{n=0}^{\infty}\frac1{(n+1)^2} \\ &= \sum_{n=1}^\infty \frac{1}{n^2}\end{aligned}$$