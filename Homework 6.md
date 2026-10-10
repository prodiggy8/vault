---
tags:
  - calculus
type:
author:
description:
aliases:
date created: Friday, October 9th 2026, 4:40:30 pm
date modified: Friday, October 9th 2026, 4:40:33 pm
---
### Problem 1
W.l.o.g. center the sphere at origin and say it has radius $a > 0$. The sphere is then the level surface:
$$F(x,y,z)=x^2+y^2+z^2=a^2$$
At at any point where $\nabla F \neq 0$, $\nabla F$ is normal to the surface:
$$\nabla F(x,y,z)=\left( \frac{\partial F}{\partial x}, \frac{\partial F}{\partial y}, \frac{\partial F}{\partial z} \right)=(2x,2y,2z)=2(x,y,z)=2r$$
Where $r$ is the position vector of the point. On the sphere, $|r|=a > 0$ so $\nabla F = 2r \neq 0$. The normal then is defined everywhere. The radius from the center to $(x,y,z)$ is $r$ so the radius is a scalar multiple of the normal vector.   

### Problem 2
For $f,g : \mathbb{R}^n \rightarrow \mathbb{R}$
$$
\begin{align}
\nabla(fg)=(\dfrac{\partial fg}{\partial x_{1}},\dots, \dfrac{\partial fg}{\partial x_{n}}) \\
\frac{\partial fg}{\partial x_{i}}=\frac{\partial f}{\partial x_{i}}g + \frac{\partial g}{\partial x_{i}}f \\
\nabla(fg)=(\dfrac{\partial f}{\partial x_{1}}g,\dots, \dfrac{\partial f}{\partial x_{n}}g) + (\dfrac{\partial g}{\partial x_{1}}f,\dots, \dfrac{\partial g}{\partial x_{n}}f)=\nabla f \cdot g + \nabla g \cdot f
\end{align}
$$


### Problem 3
The gradient of $f$ is $\nabla f(x, y) = (2x,\ 4y)$. Writing $\vec r(t) = \langle x(t), y(t) \rangle$, the condition $\vec r\,'(t) = -\nabla f(\vec r(t))$ splits into two separate differential equations,

$$
x'(t) = -2x(t), \qquad y'(t) = -4y(t),
$$

with initial conditions $x(0) = x_0$ and $y(0) = y_0$.

Solving equations:

$$
\frac{1}{x}\,\frac{dx}{dt} = -2.
$$

$$
\int \frac{1}{x}\,dx = \int -2\,dt \quad\Longrightarrow\quad \ln|x| = -2t + C.
$$

$$
|x| = e^{C} e^{-2t} \quad\Longrightarrow\quad x(t) = A\,e^{-2t},
$$

where $A$ is a constant. Setting $t = 0$ gives $x(0) = A = x_0$, so

$$
x(t) = x_0\,e^{-2t}.
$$
Similarly:
$$
y(t) = y_0\,e^{-4t}.
$$

The curve of steepest descent is therefore

$$
\vec r(t) = \left\langle x_0\,e^{-2t},\ y_0\,e^{-4t} \right\rangle.
$$

When $x_0 \neq 0$, the identity $e^{-4t} = (e^{-2t})^2 = (x/x_0)^2$ shows the path lies on the parabola

$$
y = \frac{y_0}{x_0^2}\,x^2,
$$

and it approaches the origin, where $f$ has its minimum, as $t \to \infty$. When $x_0 = 0$, the path is the segment of the $y$-axis running from $y_0$ to the origin.

### Problem 4

Let the side lengths be $a$, $b$, $c$, with $a + b + c = 1$, so the semi perimeter is $s = \tfrac{1}{2}$. By Heron's formula, the area $A$ satisfies

$$
A^2 = s(s-a)(s-b)(s-c) = \frac{1}{2}\left(\frac{1}{2}-a\right)\left(\frac{1}{2}-b\right)\left(\frac{1}{2}-c\right).
$$

We maximize:

$$
g(a, b, c) = \left(\frac{1}{2}-a\right)\left(\frac{1}{2}-b\right)\left(\frac{1}{2}-c\right)
$$

subject to the constraint $h(a, b, c) = a + b + c = 1$.

The triangle inequality forces $0 < a, b, c < \tfrac{1}{2}$ on the closed region where $a, b, c \le \tfrac12$, the function $g$ is continuous, equals zero on the boundary, and is positive inside, so its maximum occurs at an interior critical point.

The condition $\nabla g = \lambda \nabla h$, with $\nabla h = (1, 1, 1)$, gives

$$
-\left(\frac{1}{2}-b\right)\left(\frac{1}{2}-c\right) = \lambda, \qquad
-\left(\frac{1}{2}-a\right)\left(\frac{1}{2}-c\right) = \lambda, \qquad
-\left(\frac{1}{2}-a\right)\left(\frac{1}{2}-b\right) = \lambda.
$$

Equating the first two expressions,

$$
\left(\frac{1}{2}-b\right)\left(\frac{1}{2}-c\right) = \left(\frac{1}{2}-a\right)\left(\frac{1}{2}-c\right).
$$

In the interior $\tfrac{1}{2} - c > 0$, so we may divide by it to get $\tfrac{1}{2} - b = \tfrac{1}{2} - a$, that is, $a = b$. Equating the second and third expressions in the same way gives $b = c$. Combined with $a + b + c = 1$, this forces

$$
a = b = c = \frac{1}{3}.
$$

This is the only critical point in the interior, so it must be where the maximum occurs. The maximizing triangle is therefore equilateral.

### Problem 5
The critical points of

$$
SSE(m, b) = \sum_i \big(y_i - (m x_i + b)\big)^2
$$

are where both partial derivatives are zero.

$$
\begin{align}
\frac{\partial SSE}{\partial m} &= -2\sum_i x_i\big(y_i - m x_i - b\big) = -2\left( \sum_i x_i y_i - m \sum_i x_i^2 - b \sum_i x_i \right) \\
\frac{\partial SSE}{\partial b} &= -2\sum_i \big(y_i - m x_i - b\big) = -2\left( \sum_i y_i - m \sum_i x_i - n b \right).
\end{align}
$$

Setting both to zero:
$$
\begin{align}
m \sum_i x_i^2 + b \sum_i x_i = \sum_i x_i y_i \\
m \sum_i x_i + n b = \sum_i y_i
\end{align}
$$
Multiplying the first equation by $n$ and the second by $\sum_i x_i$ gives
$$
\begin{align}
n m \sum_i x_i^2 + n b \sum_i x_i = n \sum_i x_i y_i \\
m \Big(\sum_i x_i\Big)^2 + n b \sum_i x_i = \sum_i x_i \sum_i y_i
\end{align}
$$
Subtracting the second from the first eliminates $b$:
$$
n m \sum_i x_i^2 - m \Big(\sum_i x_i\Big)^2 = n \sum_i x_i y_i - \sum_i x_i \sum_i y_i,
$$
$$
m \left( n \sum_i x_i^2 - \Big(\sum_i x_i\Big)^2 \right) = n \sum_i x_i y_i - \sum_i x_i \sum_i y_i.
$$
Similarly, multiplying the first equation by $\sum_i x_i$ and the second by $\sum_i x_i^2$ gives:
$$
\begin{align}
m \sum_i x_i \sum_i x_i^2 + b \Big(\sum_i x_i\Big)^2 = \sum_i x_i \sum_i x_i y_i \\
m \sum_i x_i \sum_i x_i^2 + n b \sum_i x_i^2 = \sum_i x_i^2 \sum_i y_i
\end{align}
$$
Subtracting the first from the second:

$$
n b \sum_i x_i^2 - b \Big(\sum_i x_i\Big)^2 = \sum_i x_i^2 \sum_i y_i - \sum_i x_i \sum_i x_i y_i,
$$
$$
b \left( n \sum_i x_i^2 - \Big(\sum_i x_i\Big)^2 \right) = \sum_i x_i^2 \sum_i y_i - \sum_i x_i \sum_i x_i y_i.
$$

The coefficient $n \sum_i x_i^2 - \big(\sum_i x_i\big)^2 = n \sum_i (x_i - \bar{x})^2$ is nonzero as long as the $x_i$ are not all equal, so dividing by it gives the unique critical point

$$
m = \frac{n \sum_i x_i y_i - \sum_i x_i \sum_i y_i}{n \sum_i x_i^2 - \big(\sum_i x_i\big)^2}, \qquad\qquad
b = \frac{\sum_i x_i^2 \sum_i y_i - \sum_i x_i \sum_i x_i y_i}{n \sum_i x_i^2 - \big(\sum_i x_i\big)^2}.
$$

### Problem 6
I read the natural logarithm is used in most contexts for entropy. Anyway that doesn’t change where the maximum is. Also, we assume every $p_i > 0$. 

We maximize $H$ subject to the constraint $g(p_1, \dots, p_n) = p_1 + \cdots + p_n = 1$. Since:
$$
\begin{align}
\frac{\partial H}{\partial p_i} &= -\left( 1 \cdot \log p_i + p_i \cdot \frac{1}{p_i} \right) = -\log p_i - 1 \\
\frac{\partial g}{\partial p_i} &= 1
\end{align}
$$
We have:
$$
\begin{align}
-\log p_i - 1 &= \lambda  \\
\log p_{i}&=-1-\lambda
\end{align}
$$
This is valid for all $p_{i}$. Since $\log$ is one-to-one, it must be all the $p_i$ are equal.

