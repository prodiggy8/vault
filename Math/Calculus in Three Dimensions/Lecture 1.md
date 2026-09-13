---
tags:
type:
author:
description:
aliases:
date created: Monday, August 31st 2026, 12:04:07 am
date modified: Saturday, September 12th 2026, 12:38:46 pm
---
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