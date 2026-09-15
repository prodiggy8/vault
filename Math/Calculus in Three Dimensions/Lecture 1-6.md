---
tags:
type:
author:
description:
aliases:
date created: Monday, August 31st 2026, 12:04:07 am
date modified: Saturday, September 12th 2026, 12:38:46 pm
---
### Rotations

Polar coordinates:
$$
\begin{align}
r = \sqrt{ x^2 + y^2 } \\
\theta = \arctan\left( \frac{y}{x} \right) \\
x = r\cos \theta \\
y = r\sin \theta
\end{align}
$$
Distance between two polar coordinates:
$$
d = \sqrt{ r_{1}^2 + r_{2}^2 - 2r_{1}r_{2}\cos(\theta_{2}-\theta_{1})}
$$

Rotating $(x,y)$ by an angle $\phi$ about the origin, generating $(x’, y’)$.

- Express $(x, y)$ as $(r, \theta)$ and $(x’, y’)$ as $(r', \theta')$
- Since we are rotating around the origin, $r=r'$
- $\theta'=\theta+\phi$

Now, we just convert back (last step is just substituting polar coordinate)

$$
x' = r' \cos \theta'=r\cos(\theta+\phi)=r\cos \theta \cos \phi - r\sin \theta \sin \phi= x\cos \phi-y\sin \phi
$$

$$
y'=r' \sin \theta' = r\cos(\theta + \phi) = r\cos \theta \sin \phi + r\sin \theta \cos \phi=x\sin \phi+y\cos \phi
$$

To do the inverse and get $(x,y)$ we just rotate by $- \phi$.

___
### Right hand rule

Point the thumb of your *right* hand in the direction of the orientation of the axis. How the fingers curl indicates the positive direction of rotation.

A positive rotation about the $+z$-axis rotates the $+x$-axis into the  $+y$-axis and leaves the $+z$-axis unchanged.
$$
\begin{align}
x'=x\cos \theta - y \sin \theta  \\
y'=x\sin \theta + y \cos \theta  \\
z'=z
\end{align}
$$
A positive rotation about the $+x$-axis rotates the $+y$-axis into the $+z$-axis:
$$
\begin{align}
x'=x \\
y'=y\cos \theta - z \sin \theta \\
z'=y\sin \theta + z\cos \theta
\end{align}
$$
A positive rotation about the $+y$-axis rotates the $+z$-axis into the $+x$-axis:
$$
\begin{align}
x' = z\sin \theta + x\cos \theta \\
y' = y \\
z' = z\cos \theta - x \sin \theta
\end{align}
$$

3D rotations are **non-cumulative**, the order in which we perform rotations matters.

___
## Rotating 2D vectors

Given $\langle x, y \rangle$:
$$
\langle x \cos \theta - y \sin \theta, x \sin \theta + y \cos \theta \rangle = \langle x, y \rangle  \cos \theta + \langle -y, x \rangle \sin \theta
$$

___
### Rotating 3D vectors

Want to rotate $\vec{u}$ and $\vec{v}$ by $\phi$.

Define $\operatorname{rot}_{\vec{u}}\vec{v}$ to be the vector obtained by rotating $\vec{v} - \operatorname{proj}_{\vec{u}}\vec{v}$ by $90 \degree$.
