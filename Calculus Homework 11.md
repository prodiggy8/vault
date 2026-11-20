---
tags:
type:
author:
description:
aliases:
date created: Thursday, November 19th 2026, 7:39:35 pm
date modified: Thursday, November 19th 2026, 8:09:04 pm
---

### Problem 1

Since $d\vec r=\vec v\,dt$, the work is

$$
W=\int_C\vec F\cdot d\vec r
=q\int_{t_0}^{t_1}(\vec v\times\vec B)\cdot\vec v\,dt
$$

which is $0$ because $\vec v\times\vec B$ is perpendicular to $\vec v$, so the magnetic forces do not work.

### Problem 2

Since the fields are conservative, write $\vec F_1=-\nabla\phi_1$ and $\vec F_2=-\nabla\phi_2$. Then ($\nabla$ is linear):

$$
\vec F_1+\vec F_2
=-\nabla\phi_1-\nabla\phi_2
=-\nabla(\phi_1+\phi_2)
$$

Thus their sum is conservative, with potential $\phi_1+\phi_2$.

### Problem 3

For $\rho=\sqrt{x^2+y^2+z^2}>0$,

$$
\hat\rho=\frac{(x,y,z)}{\rho}
\qquad
\phi=-\frac1\rho=-(x^2+y^2+z^2)^{-1/2}
$$

By  chain rule,

$$
\frac{\partial\phi}{\partial x}
=\frac12(x^2+y^2+z^2)^{-3/2}(2x)
=\frac{x}{\rho^3}
$$

$$
\frac{\partial\phi}{\partial y}=\frac{y}{\rho^3}
\qquad
\frac{\partial\phi}{\partial z}=\frac{z}{\rho^3}
$$

$$
-\nabla\phi
=-\frac{(x,y,z)}{\rho^3}
=-\frac1{\rho^2}\hat\rho
=\vec F
$$

so $\phi$ is a potential function away from the origin.

### Problem 4

##### a)

The combined potential is

$$
\phi_d=
\frac{1}{\sqrt{x^2+y^2+(z-d/2)^2}}
-\frac{1}{\sqrt{x^2+y^2+(z+d/2)^2}}
$$

The limit becomes i.f., so we use Lhopital’s:

$$
\begin{aligned}
\phi
&=\lim_{d\to0}\frac{\phi_d}{d}\\
&=\lim_{d\to0}\left[
\frac{z-d}{2[x^2+y^2+(z-d)^2]^{3/2}}
+\frac{z+d/2}{2[x^2+y^2+(z+d/2)^2]^{3/2}}
\right]\\
&=\frac{z}{2(x^2+y^2+z^2)^{3/2}}
+\frac{z}{2(x^2+y^2+z^2)^{3/2}}\\
&=\frac{z}{(x^2+y^2+z^2)^{3/2}}
\end{aligned}
$$

##### b)

Let $r=\sqrt{x^2+y^2+z^2}$. Differentiating $\phi=zr^{-3}$,

$$
\frac{\partial\phi}{\partial x}=-\frac{3xz}{r^5}
\qquad
\frac{\partial\phi}{\partial y}=-\frac{3yz}{r^5}
\qquad
\frac{\partial\phi}{\partial z}
=\frac1{r^3}-\frac{3z^2}{r^5}
$$

Therefore,

$$
\vec E=-\nabla\phi
=\frac{(3xz,\;3yz,\;2z^2-x^2-y^2)}
{(x^2+y^2+z^2)^{5/2}}
$$

##### c)

In the $xz$-plane,

$$
\vec E(x,0,z)
=\frac{(3xz,\;0,\;2z^2-x^2)}{(x^2+z^2)^{5/2}}.
$$

![[Calculus Homework 11-1.png|288]]

On the $x$-axis,

$$
\vec E(x,0,0)=-\frac{1}{|x|^3}\hat z,
$$

so the strength is $1/|x|^3$, directed down. On the $z$-axis,

$$
\vec E(0,0,z)=\frac{2}{|z|^3}\hat z,
$$

so the strength is $2/|z|^3$, directed up.

### Problem 5

##### a)

Let $P_0 = (x_0, y_0, 0)$ be the point below the observation point. The charges at $P_0 + (a, b, 0)$ and $P_0 - (a, b, 0)$ are equal and equidistant, so their horizontal field components cancel. $$E_x = E_y = 0$$ The plane is unchanged by horizontal translations, so $\vec{E}$ can't depend on $x$ or $y$. $$\vec{E}(x, y, z) = E_z(z)\,\hat{z}$$
##### b)

The rectangle has charge $dq=dx\,dy$. The displacement from $(x,y,0)$ to $(0,0,z)$ is

$$
\vec R=(-x,-y,z)
\qquad
R=\sqrt{x^2+y^2+z^2}
$$

Treating the rectangle as a point charge,

$$
d\vec E=\frac{dq}{R^2}\frac{\vec R}{R}
=\frac{(-x,-y,z)}{(x^2+y^2+z^2)^{3/2}}\,dx\,dy
$$

In particular,

$$
dE_z=\frac{z}{(x^2+y^2+z^2)^{3/2}}\,dx\,dy
$$

##### c)

Conver to polar:

$$
\begin{aligned}
E_z
&=\int_{-\infty}^{\infty}\int_{-\infty}^{\infty}
\frac{z}{(x^2+y^2+z^2)^{3/2}}\,dx\,dy\\
&=\int_0^{2\pi}\int_0^\infty
\frac{zr}{(r^2+z^2)^{3/2}}\,dr\,d\theta\\
&=2\pi z\int_0^\infty\frac{r}{(r^2+z^2)^{3/2}}\,dr.
\end{aligned}
$$

Let $u=r^2+z^2$, so $du=2r\,dr$:

$$
\begin{aligned}
E_z
&=\pi z\int_{z^2}^\infty u^{-3/2}\,du\\
&=\pi z\left[-2u^{-1/2}\right]_{z^2}^\infty\\
&=\pi z\left(0+\frac{2}{\sqrt{z^2}}\right)\\
&=\frac{2\pi z}{|z|}.
\end{aligned}
$$

Thus:

$$
E_z=
\begin{cases}
2\pi, & z>0,\\
-2\pi, & z<0.
\end{cases}
$$

### Problem 6

Let $r=\sqrt{x^2+y^2}>0$. Since $\hat r=(x/r,y/r)$,
$$
F_x=f(r)\frac{x}{r},
\qquad
F_y=f(r)\frac{y}{r}.
$$
Using $\partial r/\partial x=x/r$ and $\partial r/\partial y=y/r$,
$$
\begin{aligned}
\frac{\partial F_x}{\partial y}
&=x\left[f'(r)\frac{y}{r}\frac1r
-f(r)\frac1{r^2}\frac{y}{r}\right]\\
&=\frac{xyf'(r)}{r^2}-\frac{xyf(r)}{r^3},
\end{aligned}
$$
and
$$
\begin{aligned}
\frac{\partial F_y}{\partial x}
&=y\left[f'(r)\frac{x}{r}\frac1r
-f(r)\frac1{r^2}\frac{x}{r}\right]\\
&=\frac{xyf'(r)}{r^2}-\frac{xyf(r)}{r^3}.
\end{aligned}
$$
Therefore $\partial F_x/\partial y=\partial F_y/\partial x$, as required.