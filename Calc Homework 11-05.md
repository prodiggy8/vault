---
tags:
type:
author:
description:
aliases:
date created: Thursday, November 5th 2026, 8:57:23 pm
date modified: Thursday, November 5th 2026, 8:57:32 pm
---
### Problem 1
Change variables to: $u = PV$ and $w = PV^\gamma$
Then the region becomes the rectangle $T_1 \le u \le T_2$, $a \le w \le b$.

The map is one-to-one, since $w/u = V^{\gamma-1}$ gives $V = (w/u)^{1/(\gamma-1)}$ and then $P = u/V$.

Jacobian:

$$\frac{\partial(u,w)}{\partial(P,V)} = \begin{vmatrix} V & P \\ V^\gamma & \gamma P V^{\gamma-1} \end{vmatrix} = \gamma P V^\gamma - P V^\gamma = (\gamma-1)PV^\gamma = (\gamma - 1)w$$

So $dP\,dV = \dfrac{du\,dw}{(\gamma-1)w}$, and area is:
$$\begin{aligned} A &= \int_{T_1}^{T_2}\int_a^b \frac{1}{(\gamma-1)w}\,dw\,du \\  
&= \frac{1}{\gamma-1}\int_{T_1}^{T_2}\Big[\log w\Big]_a^b\,du \\  
&= \frac{1}{\gamma-1}\int_{T_1}^{T_2}(\log b - \log a)\,du \\  
&= \frac{1}{\gamma-1}\log\frac ba\,\Big[u\Big]_{T_1}^{T_2} \\  
&= \frac{1}{\gamma-1}(T_2 - T_1)\log\frac{b}{a}.  
\end{aligned}  
$$

### Problem 2
Parametrize the sphere with spherical coordinates:

$$\mathbf r(\phi,\theta) = (R\sin\phi\cos\theta,\ R\sin\phi\sin\theta,\ R\cos\phi), \quad 0\le\theta\le 2\pi.$$

The standard computation gives $|\mathbf r_\phi \times \mathbf r_\theta| = R^2\sin\phi$.

The condition $z \ge R - h$ means $\cos\phi \ge 1 - \frac{h}{R}$, so $0 \le \phi \le \phi_0$ with $\cos\phi_0 = 1 - \frac hR$.

$$A = \int_0^{2\pi}\int_0^{\phi_0} R^2 \sin\phi\,d\phi\,d\theta = 2\pi R^2(1 - \cos\phi_0) = 2\pi R^2\cdot\frac{h}{R} = 2\pi R h.$$

The sphere is symmetric under rotation, so we can rotate the planes to be horizontal: $z = c_1$ and $z = c_2$ with $-R \le c_1 < c_2 \le R$.

First, the area of $\{z \ge c\}$ equals $2\pi R(R - c)$ for every $c \in [-R, R]$:

- If $c \ge 0$, it is a cap of height $h = R - c \le R$, so the area is $2\pi R(R-c)$.
- If $c < 0$, it is the whole sphere minus the cap $\{z \le c\}$. By symmetry that cap has height $R + c \le R$, so the area is $4\pi R^2 - 2\pi R(R + c) = 2\pi R(R - c)$.

So the band between the two planes has area

$$2\pi R(R - c_1) - 2\pi R(R - c_2) = 2\pi R(c_2 - c_1).$$

This depends only on the distance $c_2 - c_1$ between the planes, not on where they cut the sphere.

### Problem 3
Cylindrical coordinates $(r, \theta, z)$, with $dV = r\,dr\,dz\,d\theta$
The torus is $(r - R)^2 + z^2 \le a^2$, $0 \le \theta \le 2\pi$.

For fixed $z$ with $-a \le z \le a$, solving $(r-R)^2 \le a^2 - z^2$ gives

$$R - \sqrt{a^2 - z^2} \le r \le R + \sqrt{a^2 - z^2}.$$

Since $a \le R$, the lower bound is $\ge 0$. Write $s = \sqrt{a^2 - z^2}$ to shorten the limits.

Two one-variable integrals will be needed. With $z = a\sin t$, $dz = a\cos t\,dt$, $-\frac\pi2 \le t \le \frac\pi2$, and $\sqrt{a^2 - z^2} = a\cos t$:

$$\int_{-a}^{a}\sqrt{a^2 - z^2}\,dz = a^2\int_{-\pi/2}^{\pi/2}\cos^2 t\,dt = a^2\int_{-\pi/2}^{\pi/2}\frac{1 + \cos 2t}{2}\,dt = \frac{\pi a^2}{2},$$ $$\int_{-a}^{a}(a^2 - z^2)^{3/2}\,dz = a^4\int_{-\pi/2}^{\pi/2}\cos^4 t\,dt.$$

For $\cos^4 t$, apply the half-angle identity twice:

$$\cos^4 t = \left(\frac{1 + \cos 2t}{2}\right)^2 = \frac{1 + 2\cos 2t + \cos^2 2t}{4} = \frac{1 + 2\cos 2t + \frac{1 + \cos 4t}{2}}{4} = \frac38 + \frac12\cos 2t + \frac18\cos 4t.$$

Since $\sin 2t$ and $\sin 4t$ vanish at $t = \pm\frac\pi2$,

$$\int_{-\pi/2}^{\pi/2}\cos^4 t\,dt = \frac38\cdot\pi = \frac{3\pi}{8}, \qquad\text{so}\qquad \int_{-a}^{a}(a^2 - z^2)^{3/2}\,dz = \frac{3\pi a^4}{8}.$$

Mass (density $1$):

$$  
\begin{aligned}  
M &= \int_0^{2\pi}\int_{-a}^{a}\int_{R - s}^{R + s} r\,dr\,dz\,d\theta \\  
&= 2\pi\int_{-a}^{a}\left[\frac{r^2}{2}\right]_{R-s}^{R+s}dz \\  
&= \pi\int_{-a}^{a}\left((R + s)^2 - (R - s)^2\right)dz \\  
&= \pi\int_{-a}^{a} 4Rs\,dz \\  
&= 4\pi R\int_{-a}^{a}\sqrt{a^2 - z^2}\,dz \\  
&= 4\pi R\cdot\frac{\pi a^2}{2} = 2\pi^2 R a^2.  
\end{aligned}  
$$

Moment of inertia about the $z$-axis, where the distance to the axis is $r$:

$$  
\begin{aligned}  
I_z &= \iiint r^2\,dV = \int_0^{2\pi}\int_{-a}^{a}\int_{R - s}^{R + s} r^3\,dr\,dz\,d\theta \\  
&= 2\pi\int_{-a}^{a}\left[\frac{r^4}{4}\right]_{R-s}^{R+s}dz \\  
&= \frac\pi2\int_{-a}^{a}\left((R + s)^4 - (R - s)^4\right)dz.  
\end{aligned}  
$$

By the binomial theorem, the even powers of $s$ cancel:

$$(R + s)^4 - (R - s)^4 = 8R^3 s + 8R s^3.$$

So

$$  
\begin{aligned}  
I_z &= \frac\pi2\int_{-a}^{a}\left(8R^3\sqrt{a^2 - z^2} + 8R(a^2 - z^2)^{3/2}\right)dz \\  
&= 4\pi R^3\cdot\frac{\pi a^2}{2} + 4\pi R\cdot\frac{3\pi a^4}{8} \\  
&= 2\pi^2 R^3 a^2 + \frac32\pi^2 R a^4.  
\end{aligned}  
$$

In terms of the mass:

$$I_z = 2\pi^2 R a^2\left(R^2 + \frac34 a^2\right) = M\left(R^2 + \frac34 a^2\right).$$