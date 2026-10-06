---
tags:
  - calculus
type:
author:
description:
aliases:
date created: Monday, October 5th 2026, 6:42:48 pm
date modified: Monday, October 5th 2026, 6:42:54 pm
---
## Quadric Surfaces

Any equations of the form $Ax^2 + By^2 + Cz^2 + Dxy + Exz + Fyz + Gx + Hy + Iz + J = 0$

#### Ellipsoid
$$\left( \frac{x}{a} \right)^2 + \left( \frac{y}{b} \right)^2 + \left( \frac{z}{c} \right)^2=1$$
Note that if $a=b=c$ we have a sphere!

##### Cone
$$\left( \frac{x}{a} \right)^2 + \left( \frac{y}{b} \right)^2 = \left( \frac{z}{c} \right)^2$$
It’s shaped like an hourglass.

If we want only the top of bottom half we can solve the equation for $z$:
$$z^2=\frac{c^2}{a^2}x^2+\frac{c^2}{b^2}y^2$$
$$z=\pm \sqrt{ A^2x^2 + B^2y^2 }$$
For each portion hourglass we just change the sign.

Note that this cone opens to the $z$-axis. The variable on the right side always determines where the cone will open to.

#### Cylinder
$$\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1$$
The cylinder will be centered on the axis corresponding to the variable that **does not** appear on the equation.

## Limits

In two dimensions, there’s only two directions we can check for a limit: from the left and from the right. With functions of two variables there are a lot more paths we need to check.

1. Plug the numbers, if you get a number that’s the answer
2. We can also do regular factoring

The cases where the above works are rare.

3. Find **different paths** to approach the point that give different values for the limit.

For instance:
$$\lim_{ (x,y) \to (0,0) } \frac{x^2y^2}{x^4 + 3y^4}$$
We can approach from the $x$-axis since $0,0$ is on the $x$-axis.
$$\lim_{ (x,0) \to (0,0)} = \frac{x^2 \cdot 0}{x^4 + 0}=0$$
The same can be done from the $y$-axis.
Another way is to look at the path $y=x$.
$$
\lim_{ (x,x) \to (0,0) } \frac{x^4}{x^4 + 3x^4}=\frac{1}{4}
$$
Hence, limit does not exist!


