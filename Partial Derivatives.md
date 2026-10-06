---
tags:
type:
author:
description:
aliases:
date created: Monday, October 5th 2026, 10:21:39 pm
date modified: Monday, October 5th 2026, 10:21:43 pm
---
Notation:
$$\dfrac{\partial f}{\partial x} \text{ or } f_{x}$$
$$\dfrac{\partial^2 f}{\partial x^2} \text{ or } f_{x x}$$
$$\dfrac{\partial^2 f}{\partial y \partial x}=\dfrac{\partial f}{\partial y} \left[ \dfrac{\partial f}{\partial x} \right] \text{ or } f_{xy}$$
Is the mixed partial derivative.

Also, as long as mixed partial derivatives are continuous, $f_{xy}=f_{yx}$.

## Chain Rule

Suppose we have $x=x(t)$ and $y=y(t)$ and $z=f(x,y)$, then:
$$
\frac{dz}{dt}=\dfrac{\partial z}{\partial x} \cdot \frac{dx}{dt} + \dfrac{\partial z}{\partial y} \cdot \frac{dy}{dt}
$$

For two independent variables like $x=x(u,v)$ and $y=y(u,v)$ and $z=f(x,y)$ we have:
$$
\frac{\partial z}{\partial u} = \frac{\partial z}{\partial x} \frac{\partial x}{\partial u} + \frac{\partial z}{\partial y} \frac{\partial y}{\partial u}
$$
$$
\frac{\partial z}{\partial v} = \frac{\partial z}{\partial x} \frac{\partial x}{\partial v} + \frac{\partial z}{\partial y} \frac{\partial y}{\partial v}$$
## Implicit Differentiation

Example:
$$
\begin{align}
\frac{d}{dx}(x^2 + 3y^2 + 4y - 4) &= \frac{d}{dx}0\\
2x + 6y \frac{dy}{dx} + 4\frac{dy}{dx} &=0 \\
\frac{dy}{dx}&=-\frac{2x}{6y+4}
\end{align}
$$
**On functions of two or more variables:**

