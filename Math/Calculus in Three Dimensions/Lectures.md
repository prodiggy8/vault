---
tags:
type:
author:
description:
aliases:
date created: Monday, August 31st 2026, 12:04:07 am
date modified: Monday, August 31st 2026, 12:04:14 am
---
### Lecture 1

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

### Lecture 2

###### Right-hand rule
- Thumb points at the z-axis
- Fingers align with the x-axis
- Fingers curl towards the y-axis

Each pair of axes forms a coordinate plane: the xy-plane, the xz-plane, and the yz-plane.

If two points lie in the same plane it’s straightforward to calculate a distance. If they don’t:
$$
d=\sqrt{(x_{2}-x_{1})^2 +(y_{2}-y_{1})^2 + (z_{2}-z_{1})^2 }
$$
A sphere with center $(a,b,c)$ and radius $r$ is defined as:
$$
(x-a)^2 + (y-b)^2 + (z-c)^2 = r^2
$$
