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
-\frac{1}{2}
\end{bmatrix} \\
 \\
(x_{1}, y_{1} ) &= \left( \frac{1}{2}, -1 \right) - 0.1 \cdot \left( -\frac{5}{2}, -\frac{1}{2} \right) \\
&= \left( \frac{3}{4},  \right)
\end{align}
$$