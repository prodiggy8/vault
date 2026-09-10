---
title: "Homework 1"
author: "Gustavo Grancieiro Ramalho"
fontsize: 11pt
geometry: margin=1in
papersize: letter
monofont: "JetBrainsMono Nerd Font Mono"
mainfont: "Inter"
linestretch: 1.15
---

#### Problem 1

Line $x-2=\frac{y-2}{3}=2z+1$ and plane $x-3y-z=-2$

$$x-2=\frac{y-2}{3}=\frac{z+\frac{1}{2}}{\frac{1}{2}} \implies d=\langle 1, 3, \frac{1}{2} \rangle=\langle 2, 6, 1 \rangle$$
$$n=\langle 1, -3, -1 \rangle$$
$$
\begin{aligned}
d \cdot n &= 2 + 6 \cdot -3 + 1 \cdot -1 = -17 \\
|d| &= \sqrt{4+36+1} = \sqrt{ 41 } \\
|n| &= \sqrt{1+9+1}=\sqrt{ 11 } \\
\cos \theta &= \frac{dn}{|d||n|}=-\frac{17}{\sqrt{ 41 }\sqrt{ 11 }} \\
\theta&=\arccos\left( \frac{17}{\sqrt{ 451 }} \right) \approx 36.8 \degree
\end{aligned}
$$
Hence, the angle is approximately $90 \degree - 36.8 \degree = 53.2 \degree$.

#### Problem 2

Reflect $(1, -3, 2)$ across the plane $3x-2y+z=-1$. We find the normal and the parametric equation, then plug:
$$n = (3, -2, 1)$$
$$
\begin{aligned}
x=x_{0}+at=1+3t && y=y_{0} + bt=-3-2t && z=z_{0} + ct = 2 + t
\end{aligned}
$$
$$
\begin{aligned}
3(1+3t) - 2(-3-2t) + (2+t) & =-1 \\
3 + 9t + 6 + 4t + 2 + t &= -1 \\
11 + 14t &=-1 \implies t = -\frac{6}{7}
\end{aligned}
$$
The reflection is the same distance past the plane so we use $t=-\frac{12}{7}$.
$$R=\left( 1-\frac{36}{7}, -3 + \frac{24}{7}, 2-\frac{12}{7} \right) = \left( -\frac{29}{7}, \frac{3}{7}, \frac{2}{7} \right)$$

#### Problem 3

Show that $-x-6=\frac{y}{2}-5=3z+6$ and $2x=\frac{y+2}{3}=-z-4$ intersect. Find equation of the plane that contains them.

$$
\begin{aligned}
x=&-t-6 && y=&2t+10 && z =& \frac{t}{3}-2 \\
x=&\frac{s}{2} && y =& 3s-2 && z =& -s-4
\end{aligned}
$$
$$
\begin{aligned}
d_{1} = \langle -1, 2, \frac{1}{3} \rangle=\langle-3,6,1 \rangle &&  d_{2}=\langle \frac{1}{2}, 3, -1 \rangle = \langle 1, 6, -2 \rangle
\end{aligned}
$$
$$
\begin{aligned}
-t-6=\frac{s}{2} && 2t+10=3s-2 && \frac{t}{3}-2 = -s - 4 \\
\end{aligned}
$$
Solve x, plug in y.
$$
\begin{aligned}
s=-2t-12 \\
2t + 10 = 3(-2t - 12) - 2 = -6y-38 \implies 8t=-48 \implies t = -6 \\ s=0
\end{aligned}
$$
So they intersect, now the equation. Nomrla of the plane we find perpendicular to both lines, we do the cross product.
$$
\begin{aligned}
\langle  a_{1}, a_{2}, a_{3} \rangle \times \langle b_{1}, b_{2}, b_{3} \rangle &= \langle a_{2} b_{3} - a_{3} b_{2}, a_{3} b_{1} - a_{1}b_{3}, a_{1}b_{2} = a_{2}b_{1} \rangle \\
x&=6 \cdot -2 - 6 = -12-6=-18\\
y&=1 - (-3)(-2)=1-6=-5 \\
z&=(-3)6 - 6 = -18 - 6 = -24 \\
n&= \langle -18, -5, -24 \rangle
\end{aligned}
$$
Hence
$$
\begin{aligned}
-18(x-0)-5(y+2)-24(z+4)&=0\\
-18x-5y-10-24z-96&=0 \\
-18x-5y-24z&=106
\end{aligned}
$$

#### Problem 3