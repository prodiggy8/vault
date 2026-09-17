---
tags:
type:
author:
description:
aliases:
date created: Thursday, September 17th 2026, 11:14:57 am
date modified: Thursday, September 17th 2026, 11:15:12 am
---

Formulas:
$$
\begin{align}
\sin 2t=2\sin t\cos t \\
\cos 2t=\cos^2t-\sin^2t \\
1-\cos t=2\sin^2\left( \frac{t}{2} \right) \\
1+\cos t=2\cos^2\left( \frac{t}{2} \right) \\
\sin t=2\sin\left( \frac{t}{2} \right)\cos\left( \frac{t}{2} \right)
\end{align}
$$
#### Problem 1

The $x$ covered equals the arc rolled and the radius is $1$ so the center is at $\vec{C}(t)=\langle t,1\rangle$.

Relative to the center, the point starts at $\vec{v}=\langle 0,-1,0\rangle$. Rolling right is clockwise, so $\vec{u}=\langle 0,0,-1\rangle$, $|\vec{u}|=1$. Then $\operatorname{proj}_{\vec{u}}\vec{v}=\vec{0}$ and $\operatorname{rot}_{\vec{u}}\vec{v}=\vec{u}\times\vec{v}=\langle -1,0,0\rangle$, so the rotation formula gives
$$\begin{align} \langle 0,-1\rangle\cos t+\langle -1,0\rangle\sin t=\langle -\sin t,-\cos t\rangle \end{align} 
$$
Adding, 
$$\begin{align} \vec{r}(t)=\langle t,1\rangle+\langle -\sin t,-\cos t\rangle=\langle t-\sin t,\ 1-\cos t\rangle \end{align} 
$$


#### Problem 2
$\vec{r}(t)=\langle t-\sin t, 1 - \cos t \rangle$ 

We use this formula:
$$
\begin{align}
\kappa&=\frac{|r' \times r''|}{|r'(t)|^3} \\
r'(t)&=\langle 1 - \cos t, \sin t,0 \rangle \\
r''(t)&=\langle \sin t, \cos t,0 \rangle   \\
\end{align}
$$
$$
\begin{align}
r'(t) \times r''(t)&=\langle 0,0,(1-\cos t)\cos t-\sin^2 t \rangle  \\
&=\langle 0, 0, \cos t - (\cos^2t + \sin^2 t) \rangle  \\
&=\langle 0, 0, \cos t - 1 \rangle 
\end{align}
$$
$$
\begin{align}
|r'(t)|^2&=(1-\cos t)^2+\sin^2t \\
&=1-2\cos t + \cos^2t + \sin^2t \\
&=1-2 \cos t + 1 \\
&=2 - 2\cos t \\
&=2 \cdot 2 \sin^2\left( \frac{t}{2} \right) \\
|r'(t)|&=2|\sin\left( \frac{t}{2} \right)| \\
|r'(t)|^3&=8|\sin^3\left( \frac{t}{2} \right)| \\
\end{align}
$$
Numerator: $|\cos t-1|=1-\cos t$
$$
\begin{align}
\kappa=\frac{1-\cos t}{8|\sin^3\left( \frac{t}{2} \right)|}=\frac{2\sin^2\left( \frac{t}{2} \right)}{8|\sin^3\left( \frac{t}{2} \right)|}=\frac{1}{4|\sin\left( \frac{t}{2} \right)|}
\end{align}
$$

Radius of the circle: $\frac{1}{\kappa}=4|\sin\left( \frac{t}{2} \right)|$
We need the normal vector for a formula:
$$
\begin{align}
T(t)&=\frac{r'(t)}{|r'(t)|}=\frac{\langle 1-\cos t,\sin t,0 \rangle}{2|\sin\left( \frac{t}{2} \right)|} =\langle \frac{2\sin^2\left( \frac{t}{2} \right)}{2|\sin\left( \frac{t}{2} \right)|}, \frac{2\sin\left( \frac{t}{2} \right)\cos\left( \frac{t}{2} \right)}{2|\sin\left( \frac{t}{2} \right)|}, 0 \rangle  \\
T(t)&=\langle \sin\left( \frac{t}{2} \right), \cos\left( \frac{t}{2} \right),0 \rangle 
\end{align}
$$
Provided $0 < t < 2\pi$
$$
\begin{align}
N(t)&=\frac{\langle \frac{1}{2}\cos\left( \frac{t}{2} \right), -\frac{1}{2}\sin\left( \frac{t}{2} \right),0 \rangle}{\sqrt{ \left( \frac{1}{2} \right)^2\left( \cos^2\left( \frac{t}{2} \right) + \sin^2\left( \frac{t}{2} \right) \right) }}  \\
&=\langle \cos\left( \frac{t}{2} \right), -\sin\left( \frac{t}{2} \right),0 \rangle
\end{align}
$$
Provided all of these, we define:
$$
\begin{align}
\vec{c}(t)&=r(t) + \frac{1}{\kappa}N(t) \\
\vec{c}(t)&=\langle t-\sin t, 1 - \cos t \rangle + 4\sin\left( \frac{t}{2} \right)\langle \cos\left( \frac{t}{2} \right), -\sin\left( \frac{t}{2} \right) \rangle  \\
\vec{c}(t)&=\langle  t + \sin t, \cos t-1\rangle 
\end{align}
$$
This is also a cycloid.

#### Problem 3

$\frac{d^2\vec{r}(t)}{dt^2}=\sin(t)\hat{x}+\cos(t)\hat{y}$ 

We integrate twice to get $r(t)$. At rest means they should both equal $0$ at $t=0$. 
$$
\begin{align}
\int x\sin t+y\cos t \; dt=-x\cos t + y\sin t+C_{1} \\
-x + C_{1}=0 \implies C_{1}=x \\
v(t)=x(1-\cos t) + y\sin t
\end{align}
$$
$$
\begin{align}
\int x-x\cos t+y\sin t \; dt=xt-x\sin t -y\cos t + C_{2} \\
-y+C_{2}=0 \implies C_{2}=y \\
r(t)=x(t-\sin t)+y(1-\cos t)
\end{align}
$$
Now the acceleration components, provided $0<t<2\pi$ so we get rid of absolute values:
$$
\begin{align}
a_{T}&=\frac{v \cdot a}{|v|} \\
v \cdot a &=(1-\cos t)\sin t+\sin t\cos t \\ 
&=\sin t -\sin t\cos t + \sin t\cos t \\
&=\sin t \\
|v|^2&=1 + \cos^2t -2\cos t + \sin^2t \\
&=2(1-\cos t) \\ 
&=4\sin^2\left( \frac{t}{2} \right) \\
|v|&=2\sin\left( \frac{t}{2} \right)
\end{align}
$$
$$
\begin{align}
a_{T}&=\frac{\sin t}{2\sin\left( \frac{t}{2} \right)}=\frac{2\sin \left( \frac{t}{2} \right)\cos\left( \frac{t}{2} \right)}{2\sin\left( \frac{t}{2} \right)}=\cos\left( \frac{t}{2} \right)
\end{align}
$$
$$
\begin{align}
a_{N}&=\frac{|v \times a|}{|v|} \\
v\times a&=\langle 0, 0, \sin^2 t - \cos t(1-\cos t) \rangle  \\ 
&=\langle 0, 0, 1-\cos t \rangle  \\
|v\times a|&=2\sin^2\left( \frac{t}{2} \right) \\
|v|&=2\sin\left( \frac{t}{2} \right) \\
a_{N}&=\sin\left( \frac{t}{2} \right)
\end{align}
$$
#### Problem 4

We know $\vec{F}=m\vec{a}=mv'(t)$ and $F=v \times B$
$$\begin{align}
v'(t)=v\times\hat{z}
\end{align}
$$
So $v$ is rotating with angular velocity $u=-\hat{z}=\langle 0,0,-1\rangle$.

With $\vec{v}(0)=\langle 0,1,0\rangle$:
$$\begin{align}
\operatorname{proj}_{\vec{u}}\vec{v}(0)&=\vec{0} \\
\operatorname{rot}_{\vec{u}}\vec{v}(0)&=\vec{u}\times\vec{v}(0)=\langle 0,0,-1\rangle\times\langle 0,1,0\rangle=\langle 1,0,0\rangle
\end{align}
$$
By the rotation formula,
$$
\begin{align}
\vec{v}(t)=\langle 0,1,0\rangle\cos t+\langle 1,0,0\rangle\sin t=\langle \sin t,\ \cos t,\ 0\rangle
\end{align}
$$
$$\begin{align} \vec{r}(t)=\int\vec{v}(t)\,dt=\int\langle \sin t,\ \cos t,\ 0\rangle\,dt=\langle -\cos t,\ \sin t,\ 0\rangle+C \end{align}$$
$$
\begin{align}
\vec{r}(0)=\langle -1,0,0\rangle+C=\langle 1,0,0\rangle \implies C=\langle 2,0,0\rangle
\end{align}
$$
Hence:
$$\begin{align}
\vec{r}(t)=\langle 2-\cos t,\ \sin t,\ 0\rangle
\end{align}
$$

#### Problem 5

**(a)** 
$$
\begin{align}
\vec{\omega}(0)&=\langle 0,3,4\rangle+\langle 0,0,1\rangle=\langle 0,3,5\rangle
\end{align}
$$

**(b)**
Spin: $\vec{v}=\langle 0,3,4\rangle$ about $\vec{u}=\langle 0,0,1\rangle$
$$\begin{align}
\operatorname{proj}_{\vec{u}}\vec{v}&=\langle 0,0,4\rangle \\
\vec{v}-\operatorname{proj}_{\vec{u}}\vec{v}&=\langle 0,3,0\rangle \\
\operatorname{rot}_{\vec{u}}\vec{v}&=\frac{\vec{u}\times\vec{v}}{|\vec{u}|}=\langle 0,0,1\rangle\times\langle 0,3,4\rangle=\langle -3,0,0\rangle
\end{align}
$$
$$
\begin{align}
\langle 0,0,4\rangle+\langle 0,3,0\rangle\cos t+\langle -3,0,0\rangle\sin t=\langle -3\sin t,\ 3\cos t,\ 4\rangle
\end{align}
$$
Adding precession:
$$
\begin{align}
\vec{\omega}(t)&=\langle -3\sin t,\ 3\cos t,\ 5\rangle
\end{align}
$$
**(c)** 
$\vec{u}=\langle 0,3,4\rangle$, $|\vec{u}|=5$, $\vec{v}=\langle 1,0,0\rangle$:
$$
\begin{align}
\operatorname{proj}_{\vec{u}}\vec{v}&=\frac{\vec{u}\cdot\vec{v}}{|\vec{u}|^2}\vec{u}=\vec{0} \\
\vec{v}-\operatorname{proj}_{\vec{u}}\vec{v}&=\langle 1,0,0\rangle \\
\operatorname{rot}_{\vec{u}}\vec{v}&=\frac{\langle 0,3,4\rangle\times\langle 1,0,0\rangle}{5}=\frac{\langle 0,4,-3\rangle}{5}=\langle 0,\tfrac45,-\tfrac35\rangle
\end{align}
$$
$$\begin{align}
\vec{Q}(t)&=\vec{0}+\langle 1,0,0\rangle\cos 5t+\langle 0,\tfrac45,-\tfrac35\rangle\sin 5t=\langle \cos 5t,\ \tfrac45\sin 5t,\ -\tfrac35\sin 5t\rangle
\end{align}
$$
Rotate $Q$ around the vertical axis: $\vec{u}=\langle 0,0,1\rangle$, $|\vec{u}|=1$, $\vec{v}=\vec{Q}=\langle Q_x,Q_y,Q_z\rangle$:
$$
\begin{align}
\operatorname{proj}_{\vec{u}}\vec{Q}&=\langle 0,0,Q_z\rangle \\
\vec{Q}-\operatorname{proj}_{\vec{u}}\vec{Q}&=\langle Q_x,Q_y,0\rangle \\
\operatorname{rot}_{\vec{u}}\vec{Q}&=\langle 0,0,1\rangle\times\vec{Q}=\langle -Q_y,\ Q_x,\ 0\rangle
\end{align}
$$
$$\begin{align}
\vec{r}(t)&=\langle 0,0,Q_z\rangle+\langle Q_x,Q_y,0\rangle\cos t+\langle -Q_y,Q_x,0\rangle\sin t \\
&=\langle Q_x\cos t-Q_y\sin t,\ \ Q_x\sin t+Q_y\cos t,\ \ Q_z\rangle \\
&=\left\langle \cos t\cos 5t-\tfrac45\sin t\sin 5t,\ \ \sin t\cos 5t+\tfrac45\cos t\sin 5t,\ \ -\tfrac35\sin 5t\right\rangle
\end{align}
$$


**(d)**
Doing each term at a time for simplicity:
$$
\begin{align}
x'&=-\sin t\cos 5t-5\cos t\sin 5t-\tfrac45\cos t\sin 5t-4\sin t\cos 5t=-5\sin t\cos 5t-\tfrac{29}{5}\cos t\sin 5t \\
y'&=\cos t\cos 5t-5\sin t\sin 5t-\tfrac45\sin t\sin 5t+4\cos t\cos 5t=5\cos t\cos 5t-\tfrac{29}{5}\sin t\sin 5t \\
z'&=-3\cos 5t
\end{align}
$$
Now $\vec{\omega}\times\vec{r}$ with $\vec{\omega}=\langle -3\sin t,\ 3\cos t,\ 5\rangle$:
$$\begin{align}
(\vec{\omega}\times\vec{r})_x&=\omega_y r_z-\omega_z r_y
=3\cos t\left(-\tfrac35\sin 5t\right)-5\left(\sin t\cos 5t+\tfrac45\cos t\sin 5t\right) \\
&=-5\sin t\cos 5t-\tfrac{29}{5}\cos t\sin 5t \\
(\vec{\omega}\times\vec{r})_y&=\omega_z r_x-\omega_x r_z
=5\left(\cos t\cos 5t-\tfrac45\sin t\sin 5t\right)-(-3\sin t)\left(-\tfrac35\sin 5t\right) \\
&=5\cos t\cos 5t-\tfrac{29}{5}\sin t\sin 5t \\
(\vec{\omega}\times\vec{r})_z&=\omega_x r_y-\omega_y r_x \\
&=-3\sin t\left(\sin t\cos 5t+\tfrac45\cos t\sin 5t\right)-3\cos t\left(\cos t\cos 5t-\tfrac45\sin t\sin 5t\right) \\
&=-3(\sin^2 t+\cos^2 t)\cos 5t=-3\cos 5t
\end{align}
$$
Hence $\vec{r}\,'(t)=\vec{\omega}(t)\times\vec{r}(t)$.

