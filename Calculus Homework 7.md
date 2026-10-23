---
tags:
type:
author:
description:
aliases:
date created: Thursday, October 22nd 2026, 7:54:20 pm
date modified: Thursday, October 22nd 2026, 7:54:26 pm
---
### Problem 1

##### a) $\dfrac{\partial f}{\partial x}$
$$
\begin{align}
r &= \sqrt{ x^2 + y^2 } \\
\theta &= \arctan\left( \frac{y}{x} \right) \\ \\

\dfrac{\partial r}{\partial x} &= \frac{x}{\sqrt{ x^2 + y^2 }}=\frac{r\cos \theta}{\sqrt{ r^2(\cos^2 \theta + \sin^2 \theta)}} = \cos \theta\\
\dfrac{\partial \theta}{\partial x} &= \frac{-y}{x^2 + y^2} = \frac{-r\sin \theta}{r^2(\cos^2 \theta + \sin^2 \theta)} = \frac{-\sin \theta}{r} \\ \\

\dfrac{\partial f}{\partial x} &= \dfrac{\partial f}{\partial r}\dfrac{\partial r}{\partial x} + \dfrac{\partial f}{\partial \theta}\dfrac{\partial \theta}{\partial x} \\
&=\dfrac{\partial f}{\partial r}\cos \theta - \dfrac{\partial f}{\partial \theta} \frac{\sin \theta}{r}
\end{align}
$$
##### b) $\dfrac{\partial f}{\partial y}$
$$
\begin{align}
\dfrac{\partial r}{\partial y} &= \frac{y}{\sqrt{ x^2 + y^2 }}=\sin \theta \\
\dfrac{\partial \theta}{\partial y} &= \frac{x}{x^2 + y^2}=\frac{\cos \theta}{r} \\
 \\
\dfrac{\partial f}{\partial y} &= \dfrac{\partial f}{\partial r}\dfrac{\partial r}{\partial y} + \dfrac{\partial f}{\partial \theta}\dfrac{\partial \theta}{\partial y} \\
&= \dfrac{\partial f}{\partial r} \sin \theta + \dfrac{\partial f}{\partial \theta} \frac{\cos \theta}{r}
\end{align}
$$
##### c) $\dfrac{\partial^2 f}{\partial x^2}$

$$
\text{Let }g=\dfrac{\partial f}{\partial r}\cos \theta - \dfrac{\partial f}{\partial \theta} \frac{\sin \theta}{r}
$$
We apply the formula from a) with $g$ in place of $f$.
$$
\begin{align}
\dfrac{\partial g}{\partial r} &= \dfrac{\partial^2 f}{\partial r^2}\cos \theta -\left( \dfrac{\partial^2 f}{\partial r \partial \theta}\frac{\sin \theta}{r} - \dfrac{\partial f}{\partial \theta} \frac{\sin \theta}{r^2}\right) \\
 \\
\dfrac{\partial g}{\partial \theta} &= (\dfrac{\partial^2 f}{\partial r \partial \theta} \cos \theta - \dfrac{\partial f}{\partial r} \sin \theta) - \left( \dfrac{\partial^2 f}{\partial \theta^2} \frac{\sin \theta}{r} + \dfrac{\partial f}{\partial \theta} \frac{\cos \theta}{r} \right) \\
 \\
\cos\theta \dfrac{\partial g}{\partial r} &= \cos^2\theta\,\dfrac{\partial^2 f}{\partial r^2} - \frac{\sin\theta\cos\theta}{r}\,\dfrac{\partial^2 f}{\partial r\,\partial\theta} + \frac{\sin\theta\cos\theta}{r^2}\,\dfrac{\partial f}{\partial \theta} \\
-\frac{\sin\theta}{r}\,\dfrac{\partial g}{\partial \theta} &= -\frac{\sin\theta\cos\theta}{r}\,\dfrac{\partial^2 f}{\partial r\,\partial\theta} + \frac{\sin^2\theta}{r}\,\dfrac{\partial f}{\partial r} + \frac{\sin^2\theta}{r^2}\,\dfrac{\partial^2 f}{\partial \theta^2} + \frac{\sin\theta\cos\theta}{r^2}\,\dfrac{\partial f}{\partial \theta} \\
\\
 \\
\dfrac{\partial^2 f}{\partial x^2} &= \cos^2\theta\,\dfrac{\partial^2 f}{\partial r^2} - \frac{2\sin\theta\cos\theta}{r}\,\dfrac{\partial^2 f}{\partial r\,\partial\theta} + \frac{\sin^2\theta}{r^2}\,\dfrac{\partial^2 f}{\partial \theta^2} + \frac{\sin^2\theta}{r}\,\dfrac{\partial f}{\partial r} + \frac{2\sin\theta\cos\theta}{r^2}\,\dfrac{\partial f}{\partial \theta}
\end{align}
$$
##### d) $\dfrac{\partial^2 f}{\partial y^2}$
$$
\text{Let }g=\dfrac{\partial f}{\partial r}\sin \theta + \dfrac{\partial f}{\partial \theta} \frac{\cos \theta}{r}
$$
We apply the formula from b) with $g$ in place of $f$.
$$
\begin{align}
\dfrac{\partial g}{\partial \theta} &= (\dfrac{\partial^2 f}{\partial r \partial \theta}\sin \theta + \dfrac{\partial f}{\partial r}\cos \theta) + \left( \dfrac{\partial^2 f}{\partial \theta^2} \frac{\cos \theta}{r} - \dfrac{\partial f}{\partial \theta} \frac{\sin \theta}{r}\right) \\
 \\
\dfrac{\partial g}{\partial r} &= \dfrac{\partial^2 f}{\partial r^2} \sin \theta + \left( \dfrac{\partial^2f}{\partial r \partial \theta}\frac{\cos \theta}{r} -\dfrac{\partial f}{\partial \theta} \frac{\cos \theta}{r^2} \right) \\
 \\
\sin\theta\,\dfrac{\partial g}{\partial r} &= \sin^2\theta\,\dfrac{\partial^2 f}{\partial r^2} + \frac{\sin\theta\cos\theta}{r}\,\dfrac{\partial^2 f}{\partial r\,\partial\theta} - \frac{\sin\theta\cos\theta}{r^2}\,\dfrac{\partial f}{\partial \theta} \\
\frac{\cos\theta}{r}\,\dfrac{\partial g}{\partial \theta} &= \frac{\sin\theta\cos\theta}{r}\,\dfrac{\partial^2 f}{\partial r\,\partial\theta} + \frac{\cos^2\theta}{r}\,\dfrac{\partial f}{\partial r} + \frac{\cos^2\theta}{r^2}\,\dfrac{\partial^2 f}{\partial \theta^2} - \frac{\sin\theta\cos\theta}{r^2}\,\dfrac{\partial f}{\partial \theta} \\
 \\
\dfrac{\partial^2 f}{\partial y^2} &= \sin^2\theta\,\dfrac{\partial^2 f}{\partial r^2} + \frac{2\sin\theta\cos\theta}{r}\,\dfrac{\partial^2 f}{\partial r\,\partial\theta} + \frac{\cos^2\theta}{r^2}\,\dfrac{\partial^2 f}{\partial \theta^2} + \frac{\cos^2\theta}{r}\,\dfrac{\partial f}{\partial r} - \frac{2\sin\theta\cos\theta}{r^2}\,\dfrac{\partial f}{\partial \theta}
\end{align}
$$
##### e) $\dfrac{\partial^2 f}{\partial x^2} + \dfrac{\partial^2 f}{\partial y^2}$

From c) and d):
$$
\begin{align}
&= \cos^2\theta\,\dfrac{\partial^2 f}{\partial r^2} - \frac{2\sin\theta\cos\theta}{r}\,\dfrac{\partial^2 f}{\partial r\,\partial\theta} + \frac{\sin^2\theta}{r^2}\,\dfrac{\partial^2 f}{\partial \theta^2} + \frac{\sin^2\theta}{r}\,\dfrac{\partial f}{\partial r} + \frac{2\sin\theta\cos\theta}{r^2}\,\dfrac{\partial f}{\partial \theta}  \\
&+ \sin^2\theta\,\dfrac{\partial^2 f}{\partial r^2} + \frac{2\sin\theta\cos\theta}{r}\,\dfrac{\partial^2 f}{\partial r\,\partial\theta} + \frac{\cos^2\theta}{r^2}\,\dfrac{\partial^2 f}{\partial \theta^2} + \frac{\cos^2\theta}{r}\,\dfrac{\partial f}{\partial r} - \frac{2\sin\theta\cos\theta}{r^2}\,\dfrac{\partial f}{\partial \theta} \\
\\
\\
&= \dfrac{\partial^2 f}{\partial r^2} + \dfrac{\partial^2 f}{\partial \theta^2} \frac{1}{r^2} + \dfrac{\partial f}{\partial r} \frac{1}{r}
\end{align}
$$

### Problem 2

##### a)
$$f(x,y)=x^4-2x^2+y^2 + xy$$
$$
\begin{align}
\dfrac{\partial f}{\partial x} &= 4x^3 - 4x + y \\
\dfrac{\partial f}{\partial y} &= 2y + x \\ \\
\nabla f= \begin{bmatrix}
4x^3 - 4x + y \\
2y + x
\end{bmatrix}
\end{align}
$$
##### b)
$$
\begin{align}
\nabla f\left( \frac{1}{2}, -1 \right)&=\begin{bmatrix}
\frac{1}{2} - 2 - 1  \\
-2 + \frac{1}{2}
\end{bmatrix} = \begin{bmatrix}
-\frac{5}{2} \\
-\frac{3}{2}
\end{bmatrix} \\
 \\
(x_{1}, y_{1} ) &= \left( \frac{1}{2}, -1 \right) - 0.1 \cdot \left( -\frac{5}{2}, -\frac{3}{2} \right) \\
&= \left( \frac{3}{4}, -\frac{17}{20} \right)
\end{align}
$$
##### c)
```python
import math

def f(x, y):
	return (4*x**3 - 4*x + y), (2*y + x)

def g(xi, yi, h = 0.1):
	xj, yj = f(xi, yi)
	return (xi - h * xj), (yi - h * yj)
	
x0, y0 = (1/2), -1
x, y = 1.06, -0.53
i = 0

while not (math.isclose(x, x0, abs_tol=0.01) \
  and math.isclose(y, y0, abs_tol = 0.01)):
	x0, y0 = g(x0, y0)
	i += 1

print(i, x0, y0)
```

With this program, it took 17 iterations.

##### d)
With the same program from c) passing `h=0.05` to `g`, it took 37 iterations.

##### e)
It never converges (stopped after 1 minute of runtime, also if you print the intermediate values it bounces from one point to another forever).

That is because the learning rate is too large, which makes the algorithm overshoot the minimum, oscillating back and forth.

##### f)
It also never converges (stopped after 1 minute of runtime) to the same target from the previous questions. It converges, however, to $(-1.06, 0.53)$. That’s because $f$ is even, there’s another minimizer symmetric to the first, and this initial guess lies in that minimizer’s basin of attraction.

### Problem 3

$$
\begin{align}
\int_{0}^{\pi/4} &\int_{1}^{x^2 + 1} \frac{1}{y^2} dydx \\
&= \int_{0}^{\pi/4} \left[1-\frac{1}{x^2 + 1}\right]dx \\
&= \left( \frac{\pi}{4} \right) - \left( \arctan\left( \frac{\pi}{4} \right) - \arctan(0)\right) \\
&= \frac{\pi}{4} - \arctan\left( \frac{\pi}{4} \right)
\end{align}
$$
### Problem 4
(Omitting the limit notation)
$$
\begin{align}
\int_{0}^{\infty}\int_{0}^{\infty} xe^{-x-y}dxdy
\end{align}
$$
$$
\begin{align}
\int_{0}^{\infty}&xe^{-x-y}dx \\
\text{Let: } \\
u&=x \\
du&=dx & \\
v &=-e^{-x-y}\\
dv &=e^{-x-y}dx \\
\text{Then:} \\
\int_{0}^{\infty}xe^{-x-y}dx &= \left[-xe^{-x-y}\right]_{0}^{\infty} + \int_{0}^{\infty} e^{-x-y}\,dx \\
&= (0 - 0) + \left[-e^{-x-y}\right]_{0}^{\infty} \\
&= 0 - \left(-e^{-y}\right) \\
&= e^{-y}
\end{align}
$$
$$
\begin{align}
\int_{0}^\infty &e^{-y}dy \\
&=\left[ -e^{-y} \right]_{0}^\infty \\
&=0 - (-1) \\
&=1
\end{align}
$$
Note to professor: this homework was the most fun so far!