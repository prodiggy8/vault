---
tags:
type:
author:
description:
aliases:
date created: Thursday, September 10th 2026, 11:16:48 am
date modified: Thursday, September 10th 2026, 11:16:51 am
---
3. Write the formulas for rotating $(x, y)$ about the origin by an angle $\theta$.
- [x] Correct
$$
\begin{aligned}
x=x \cos \theta - y \sin \theta \\
y=x \sin \theta + y \cos \theta
\end{aligned}
$$
3. I rotated a point $(x, y)$ by $120 \degree$ about the origin and got the point $(2, 1)$. What was $(x, y)$?
- [x] Correct
$$
\begin{align}
x = x'\cos - \theta - y' \sin - \theta =  x' \cos \theta + y' \sin \theta \\
x= 2 \cdot \cos(120 \degree) + \sin(120 \degree)=-1+\frac{\sqrt{ 3 }}{2}\\
y = x'\sin - \theta + y' \cos - \theta = -x' \sin \theta + y' \cos \theta \\
y=-2 \cdot \frac{\sqrt{ 3 }}{2} - \frac{1}{2}=-\sqrt{ 3 } - \frac{1}{2}
\end{align}
$$
5. Find Cartesian coordinates of the point obtained by rotating $(-2,3)$ clockwise $30 \degree$ about the point $(1, -1)$.
- [ ] Correct
- [x] Incorrect
**Mistake:**
- **Clockwise** means **negative** direction
- **Counterclockwise** is just $30 \degree$
- Forgot to move back by coordinates of the point!

We make $(1, -1)$ the origin. New point: $(-3, 4)$.
$$
\begin{align}
x' = -3 \cos 30 \degree - 4 \sin 30 \degree= -\frac{3\sqrt{ 3 }}{2}-\frac{4}{2}\\
y'=-3\sin 30 \degree +4\cos 30 \degree=-\frac{3}{2} + 2\sqrt{ 3 }
\end{align}
$$

6. Curve defined by equation $(x + y)^2$ + x + 1 = 0 from lecture. Rotate this curve by an angle $\theta$ about the origin, sending each point $(x, y)$ to $(x’, y’)$, and find $\theta$ so that the rotated curve takes the form $y’=a(x’)^2 + bx’ + c$, showing that the curve is indeed a parabola.
- [x] Correct
Done in paper.
$$
y'=2\sqrt{ 2 }(x')^2 + x' + \sqrt{ 2 }
$$

7. Let $\mathbb{R}_\theta=\mathbb{R}^2 \rightarrow \mathbb{R}^2$ be the function which rotates points about the origin by angle $\theta$ in the positive direction. Using that $R_{\theta}(R_{\phi}(1,0))=R_{\theta + \phi}(1, 0)$, prove the angle sum formulas:
$$
\begin{aligned}
\cos(\theta + \phi) = \cos \theta \cos \phi - \sin \theta \sin \phi \\
\sin(\theta + \phi) = \sin \theta \cos \phi + \sin \phi \cos \theta
\end{aligned}
$$
(Note that these imply the very important double angle formulas: $\sin(2\theta)=2\sin \theta \cos \theta$ and $cos(2\theta)=\cos^2\theta-\sin^2\theta=2\cos^2\theta-1=1-2\sin^2\theta$).

8. a) Suppose (a, b) rotated by $\theta$ about the origin gives (c, d). Show that: $(a + bi)(\cos \theta + i\sin \theta)=c + di$
$$
= a\cos \theta + a \cdot i \sin \theta + bi \cos \theta - b \sin \theta
$$
$$
= (a \cos \theta - b\sin \theta) + a \cdot i \sin \theta + b i \cos \theta
$$
$$
= c + i(a \sin \theta + b \cos \theta)
$$
$$
=c + di
$$
b) Compute $\left( \cos\left( \frac{\pi}{5} \right) + i \sin\left( \frac{\pi}{5} \right) \right)^{15}$. Hint: use (a) 15 times.

This is just **rotation** by pi/5 15 times, hence
$$\cos\left( \frac{150}{5} \right) + i\sin\left( \frac{150}{\pi} \right)=-1 + 0 = -1$$

c) Compute (1-i) ^ 5

(1 - i) = (cos 3pi/2 + i sin 3pi/2 ) which is rotation by 3pi/2.

= (cos 15pi/2 + i sin 15pi/2) = i.