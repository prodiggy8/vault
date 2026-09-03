---
tags:
  - calculus
  - math
  - course/21-259
type: homework
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Thursday, September 3rd 2026, 5:07:51 pm
date modified: Thursday, September 3rd 2026, 5:07:54 pm
---
#### Problem 1

We shift by $\langle 1, -3\rangle$ and then shift back at the end.
$$\vec{v}= \langle-3-1, 5+3\rangle =\langle-4,8\rangle$$
Applying the rotation formula:
$$\begin{align}

\cos(-150\degree)=-\frac{\sqrt{ 3 }}{2} && \sin(-150 \degree)=-\frac{1}{2}

\end{align}$$
$$x'=-4 \cdot \left( -\frac{\sqrt{ 3 }}{2} \right)-8 \cdot \left( -\frac{1}{2} \right)=2\sqrt{ 3 }+4$$
$$y'=-4 \cdot \left( -\frac{1}{2} \right) + 8 \cdot \left( -\frac{\sqrt{ 3 }}{2} \right)=2-4\sqrt{ 3 }$$
$$\vec{v}' = \langle 5+ 2\sqrt{ 3 },-1-4\sqrt{ 3 }\rangle$$
#### Problem 2

$(x,y)$ rotated by $\theta$ is $(x’,y’)$ so:
$$\begin{align}
x=x' \cos \theta + y' \sin \theta && y = -x' \sin \theta + y' \cos \theta
\end{align}$$
Substituting now (writing $c$ for $\cos$ and $s$ for $sin$ for simplicity):
$$\begin{aligned}  
Ax^2=A(cx'+sy')^2 = Ac^2(x')^2 +2Acsx'y'+As^2(y')^2 \\
Bxy = B(cx'+sy')(-sx'+cy')=-Bcs(x')^2+B(c^2-s^2)x'y'+Bcs(y')^2 \\
Cy^2=C(-sx'+cy')^2=Cs^2(x')^2-2Ccsx'y'+Cc^2(y')^2 \\
Dx = Dcx' + Dsy' \\
Ey = -Esx'+Ecy' \\
F = F
\end{aligned}$$
From the above $x'y'$ coefficients are $2Acs$, $B(c^2-s^2)$ and $-2Ccs$. Their sum is the coefficient of $x’y’$ in the rotated equation.
$$B'=2Acs + B(c^2-s^2)-2Ccs=2cs(A-C) + B(c^2-s^2)$$
$$B'=2\sin \theta \cos \theta(A-C)+B(\cos^2 \theta - \sin^2 \theta)$$
$$B'=\sin 2\theta (A-C) + B \cos 2\theta$$
Setting $B'$ to $0$, provided $\cos 2 \theta$ and $C-A$ are not $0$
$$\begin{align}
(A-C)\sin 2 \theta=-B\cos 2 \theta && \frac{\sin 2 \theta}{\cos 2 \theta}=\tan 2 \theta = \frac{B}{C-A}
\end{align}$$
$$\theta=\frac{1}{2} \arctan \left( \frac{B}{C-A} \right)$$
#### Problem 3

First we convert to rectangular
$$\begin{align}
x=4 \cdot  \frac{\sqrt{ 2 }}{2}  \cdot \frac{1}{2}=\sqrt{ 2 } && y=4 \cdot \frac{\sqrt{ 2 }}{2} \cdot \frac{-\sqrt{ 3 }}{2}=-\sqrt{ 6 } && z=4 \cdot \frac{\sqrt{ 2 }}{2}=2\sqrt{ 2 }
\end{align}$$
Rotating about $+y$, $\alpha=135 \degree$, we have:
$$\begin{align}
\cos 135 \degree =-\frac{\sqrt{ 2 }}{2} && \sin(135 \degree)=\frac{\sqrt{ 2 }}{2}
\end{align}$$
$$\begin{align}
x' = z \sin \theta + x \cos \theta = 2\sqrt2\cdot\frac{\sqrt2}{2} + \sqrt2\cdot\left(-\frac{\sqrt2}{2}\right) = 1
\end{align}$$
$$y'=y=-\sqrt6$$
$$z' = z \cos \theta − x \sin \theta = 2\sqrt2\cdot\left(-\frac{\sqrt2}{2}\right) - \sqrt2\cdot\frac{\sqrt2}{2} = -3$$
Converting back:
$$\begin{align}
\rho=\sqrt{ 1+6+9 }=4 && \varphi=\arccos\left( -\frac{3}{4} \right) && \theta=-\arctan(\sqrt{ 6 })
\end{align}$$

#### Problem 4

$$\begin{align}
\rho= a\cos(\theta)\sin(\varphi) \\
\rho^2=\rho a \cos(\theta) \sin(\varphi) = ax \\
x^2+y^2+z^2=ax \\
x^2-ax+y^2+z^2=0
\end{align}$$
Completing the square:
$$\left( x-\frac{a}{2} \right)+y^2+z^2= (\frac{a}{2})^2$$
This is a sphere with center $\left( \frac{a}{2}, 0, 0 \right)$ and radius $\frac{|a|}{2}$.

#### Problem 5

Magnitude:
$$|\vec{u}|=\sqrt{ 13 }$$
Direction:
$$-\frac{\vec{v}}{|\vec{v}|}=\frac{\langle 1,1 \rangle}{\sqrt{ 2 }}$$
$$v'=-\frac{\vec{v}}{|\vec{v}|}\cdot|\vec{u|}=\langle \frac{\sqrt{ 13 }}{\sqrt{ 2 }}, \frac{\sqrt{ 13 }}{\sqrt{ 2 }}\rangle$$

#### Problem 6

Since slope is $1/2$, we rotate by $90 \degree$ to get $-\frac{1}{m}=-\frac{1}{\frac{1}{2}}=-2$
Now we just make it pass through the $(-1,2)$:
$$y-2=-2(x+1) \implies y=-2x$$

#### Problem 7

Rotate about $Q=(1,1)$ by treating it as origin. We take the point at $x=0$, $P=(0, -1)$.

$$\vec{v}=P-Q=\langle -1, -2 \rangle$$
$$\begin{align}
\cos 30 \degree=\frac{\sqrt{ 3 }}{2} && \sin 30 \degree \frac{1}{2}
\end{align}$$
$$v'=\langle -1, -2 \rangle \frac{\sqrt{ 3 }}{2} + \langle 2, -1 \rangle \frac{1}{2}$$
$$P'=Q + \vec{v}=\left( 2-\frac{\sqrt{ 3 }}{2}, \frac{1}{2} - \sqrt{ 3 } \right)$$
Now for direction using the same 2D vector rotation formula:
$$\begin{align}
d= \langle 1, 3 \rangle && d' =\frac{1}{2} \langle \sqrt{ 3 } - 3, 1 + 3\sqrt{ 3 }\rangle
\end{align}$$
$$m=\frac{1+3\sqrt{ 3 }}{\sqrt{ 3 }-3}$$
Putting it together and doing some arithmetic:
$$y-\left( \frac{1}{2} - \sqrt{ 3 }\right)=m\left( x-\left( 2-\frac{\sqrt{ 3 }}{2} \right) \right)$$
$$y=mx+m\left( \frac{\sqrt{ 3 }}{2} - 2 \right)+\frac{1}{2} - \sqrt{ 3 }$$
$$y=\frac{1+3\sqrt{ 3 }}{\sqrt{ 3 }-3}x + \frac{9+14\sqrt{ 3 }}{6}+\frac{1}{2}-\sqrt{ 3 }$$
