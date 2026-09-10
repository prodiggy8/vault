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

We shift by $\langle 1, -3\rangle$ and then shift back at the end.
$$\vec{v}= \langle-3-1, 5+3\rangle =\langle-4,8\rangle$$
Applying the rotation formula:
$$\begin{aligned}
\cos(-150 ^\circ)=-\frac{\sqrt{ 3 }}{2} && \sin(-150 ^\circ)=-\frac{1}{2}
\end{aligned}$$
$$x'=-4 \cdot \left( -\frac{\sqrt{ 3 }}{2} \right)-8 \cdot \left( -\frac{1}{2} \right)=2\sqrt{ 3 }+4$$
$$y'=-4 \cdot \left( -\frac{1}{2} \right) + 8 \cdot \left( -\frac{\sqrt{ 3 }}{2} \right)=2-4\sqrt{ 3 }$$
$$\vec{v}' = \langle 5+ 2\sqrt{ 3 },-1-4\sqrt{ 3 }\rangle$$

### Problem 2

$(x,y)$ rotated by $\theta$ is $(x’,y’)$, so we recover $(x,y)$ by rotating $(x',y')$back by $−\theta$ with
$$\begin{aligned}
x=x' \cos \theta + y' \sin \theta && y = -x' \sin \theta + y' \cos \theta
\end{aligned}$$
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
$$\begin{aligned}
(A-C)\sin 2 \theta=-B\cos 2 \theta && \frac{\sin 2 \theta}{\cos 2 \theta}=\tan 2 \theta = \frac{B}{C-A}
\end{aligned}$$
$$\theta=\frac{1}{2} \arctan \left( \frac{B}{C-A} \right)$$

If $A=C$ then $B\cos⁡2\theta=0$ so $\theta=45^\circ$; if $B=0$ take $\theta=0$. Other solutions differ by multiples of $90^\circ$.

Remaining coefficients:  
$$\begin{aligned} A'=Ac^2-Bcs+Cs^2 \\ C'=As^2+Bcs+Cc^2 \\ D'=Dc-Es \\ E'=Ds+Ec \\ F'=F \end{aligned}$$

So the rotated curve is:
$$\begin{aligned}
A'(x')2+C'(y')2+D'x'+E'y'+F'=0
\end{aligned}$$

#### Problem 3

Convert to rectangular
$$\begin{aligned}
x=4 \cdot  \frac{\sqrt{ 2 }}{2}  \cdot \frac{1}{2}=\sqrt{ 2 } && y=4 \cdot \frac{\sqrt{ 2 }}{2} \cdot \frac{-\sqrt{ 3 }}{2}=-\sqrt{ 6 } && z=4 \cdot \frac{\sqrt{ 2 }}{2}=2\sqrt{ 2 }
\end{aligned}$$
Rotating about $+y$, $\alpha=135 ^\circ$, we have:
$$\begin{aligned}
\cos 135 ^\circ =-\frac{\sqrt{ 2 }}{2} && \sin(135 ^\circ)=\frac{\sqrt{ 2 }}{2}
\end{aligned}$$
$$\begin{aligned}
x' = z \sin \theta + x \cos \theta = 2\sqrt2\cdot\frac{\sqrt2}{2} + \sqrt2\cdot\left(-\frac{\sqrt2}{2}\right) = 1
\end{aligned}$$
$$y'=y=-\sqrt6$$
$$z' = z \cos \theta − x \sin \theta = 2\sqrt2\cdot\left(-\frac{\sqrt2}{2}\right) - \sqrt2\cdot\frac{\sqrt2}{2} = -3$$
Converting back:
$$\begin{aligned}
\rho=\sqrt{ 1+6+9 }=4 && \varphi=\arccos\left( -\frac{3}{4} \right) && \theta=-\arctan(\sqrt{ 6 })
\end{aligned}$$

#### Problem 4

$$\begin{aligned}
\rho= a\cos(\theta)\sin(\varphi) \\
\rho^2=\rho a \cos(\theta) \sin(\varphi) = ax \\
x^2+y^2+z^2=ax \\
x^2-ax+y^2+z^2=0
\end{aligned}$$
Completing the square:
$$\left( x-\frac{a}{2} \right)^2+y^2+z^2= (\frac{a}{2})^2$$
This is a sphere with center $\left( \frac{a}{2}, 0, 0 \right)$ and radius $\frac{|a|}{2}$.

#### Problem 5

Magnitude:
$$|\vec{u}|=\sqrt{ 13 }$$
Direction:
$$-\frac{\vec{v}}{|\vec{v}|}=\frac{\langle 1,1 \rangle}{\sqrt{ 2 }}$$
$$v'=-\frac{\vec{v}}{|\vec{v}|}\cdot|\vec{u|}=\langle \frac{\sqrt{ 13 }}{\sqrt{ 2 }}, \frac{\sqrt{ 13 }}{\sqrt{ 2 }}\rangle$$

#### Problem 6

Since slope is $1/2$, we rotate by $90 ^\circ$ to get $-\frac{1}{m}=-\frac{1}{\frac{1}{2}}=-2$
Now we just make it pass through the $(-1,2)$:
$$y-2=-2(x+1) \implies y=-2x$$

#### Problem 7

Rotate about $Q=(1,1)$ by treating it as origin. We take the point at $x=0$, $P=(0, -1)$.

$$\vec{v}=P-Q=\langle -1, -2 \rangle$$
$$\begin{aligned}
\cos 30 ^\circ=\frac{\sqrt{ 3 }}{2} && \sin 30 ^\circ \frac{1}{2}
\end{aligned}$$
$$v'=\langle -1, -2 \rangle \frac{\sqrt{ 3 }}{2} + \langle 2, -1 \rangle \frac{1}{2}$$
$$P'=Q + \vec{v}=\left( 2-\frac{\sqrt{ 3 }}{2}, \frac{1}{2} - \sqrt{ 3 } \right)$$
Now for direction using the same 2D vector rotation formula:
$$\begin{aligned}
d= \langle 1, 3 \rangle && d' =\frac{1}{2} \langle \sqrt{ 3 } - 3, 1 + 3\sqrt{ 3 }\rangle
\end{aligned}$$
$$m=\frac{1+3\sqrt{ 3 }}{\sqrt{ 3 }-3}$$
Putting it together and doing some arithmetic:
$$y-\left( \frac{1}{2} - \sqrt{ 3 }\right)=m\left( x-\left( 2-\frac{\sqrt{ 3 }}{2} \right) \right)$$
$$y=mx+m\left( \frac{\sqrt{ 3 }}{2} - 2 \right)+\frac{1}{2} - \sqrt{ 3 }$$
$$y=\frac{1+3\sqrt{ 3 }}{\sqrt{ 3 }-3}x + \frac{9+14\sqrt{ 3 }}{6}+\frac{1}{2}-\sqrt{ 3 }$$
