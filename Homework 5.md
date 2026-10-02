## Problem 1

#### a) 
$A$ is at about $11260$
$B$ is at $10800$
$C$ is at about $11100$

#### b)
At $A$ and $C$ the horizontal partial derivative is $0$.
At $B$ it is negative.

#### c)
contour $10840$ is at about $75ft$ west and $10760$ at about $100ft$ east so that gives us $-\frac{80}{175} \approx -\frac{1}{2}$.

#### d)
At $A$ and $C$ it is negative. That’s because they are a maximums.
At $B$ it is positive because the contour is a bit closer together west than east.

#### e)
$C$ is a saddle. South of $C$, moving east goes uphill, so $\frac{\partial f}{\partial x} > 0$. North of $C$, moving east goes downhill, so $\frac{\partial f}{\partial x} < 0$. Hence, $\partial^2f/\partial y \partial x < 0$  at $C$.

## Problem 2

#### a)
Setting $x=0$ we get $0$, same for $y=0$. 
Let $x=y^2$ we get $\frac{y^4}{2y^4}=\frac{1}{2}$.
Hence, the limit does not exist.

#### b)
Let $xy=t$ then we have $\lim_{ t \to 0 } \frac{\sin(t)}{t}$.
By L’Hopital’s $=\lim_{ t \to 0 } \cos(t)=1$.

#### c)
$$\lim_{ (x,y) \to (0,0) }\frac{x^2(1+x)+y^2(1+y)}{x^2 + y^2}$$

We convert to polar coordinates:
$$
\begin{align}
&\lim_{ r \to 0 } \frac{(r\cos \theta)^2(1+r\cos \theta)+(r\sin \theta)^2(1+r\sin \theta)}{(r\cos \theta)^2 + (r\sin \theta)^2} \\
=&\lim_{ r \to 0 } \cos^2 \theta(1+r\cos \theta)+\sin^2(1+r\sin \theta) \\
=&\cos^2\theta+\sin^2\theta=1
\end{align}
$$

## Problem 3

Let $F(x,y,z) = x^2 + y^2 - z$, so a normal at $(x_0,y_0,z_0)$ is $\mathbf{n} = \nabla F = (2x_0,2y_0,-1)$, with $n\cdot n = 4z_0 + 1$.

The incoming ray has direction $d = (0,0,-1)$, and $d \cdot n = 1$, so

$$\operatorname{proj}_n d = \frac{d \cdot n}{n \cdot n}n = \frac{1}{4z_0+1}(2x_0,\ 2y_0,\ -1).$$

The reflected direction is

$$ 
\begin{align}
r &= d - 2\operatorname{proj}_n d \\ 
&= (0,0,-1) - \frac{2}{4z_0+1}(2x_0,2y_0,-1) \\
&= \frac{1}{4z_0+1}\Bigl[(0,0,-(4z_0+1)) - (4x_0,4y_0,-2)\Bigr]  \\
&= \frac{1}{4z_0+1}\bigl(-4x_0,-4y_0,1-4z_0\bigr)
\end{align}
$$

The reflected ray is $(x_0,y_0,z_0) + tr$, $t \ge 0$
Taking $t = \frac{4z_0+1}{4} > 0$:
$$
(x_0,y_0,z_0) + \tfrac14\bigl(-4x_0,\ -4y_0,\ 1-4z_0\bigr) = \left(0,\ 0,\ \tfrac14\right)$$

## Problem 4

At $(s,t)=(2,3)$, $x=g(2,3)=1$ and $y=h(2,3)=-1$. $z=f(1,-1)=3$.

$$z_{s}=f_{x} \cdot g_{s} + f_{y}\cdot h_{s}=-1 -4 =-5$$
$$z_{t}=f_{x} \cdot g_{t} + f_{y} \cdot h_{t}=3 + 4 = 7$$
We want $s=2.1$ and $t=2.95$ so $\Delta_{s}=0.1$ and $\Delta_{t} = -0.05$.
$$z \approx 3 - 5(0.1) + 7(-0.05)=3-0.5- 0.35=2.15$$

## Problem 5

We use the following formulas to get rid of variables we don’t need and then do implicit differentiation.
$$
\begin{align}
x=r\cos \theta \\
y=r\sin \theta \\
x^2+y^2=r^2 \\
x=y\cot \theta
\end{align}
$$

**1.** $\left. \frac{\partial x}{\partial y} \right|_{r}$
$$
\begin{align}
x^2 + y^2 &= r^2 \\
2x \cdot \frac{\partial x}{\partial y} + 2y &=0 \\
\frac{\partial x}{\partial y} &=-\frac{y}{x}
\end{align}
$$
**2.** $\left. \frac{\partial x}{\partial y} \right|_{\theta}$
$$
\begin{align}
x &= y\cot\theta \\
\frac{\partial x}{\partial y} &= \cot\theta \\
\frac{\partial x}{\partial y} &= \frac{x}{y}
\end{align}
$$
**3.** $\left. \frac{\partial x}{\partial r} \right|_{y}$
$$
\begin{align}
x^2 + y^2 &= r^2 \\
2x \cdot \frac{\partial x}{\partial r} &= 2r \\
\frac{\partial x}{\partial r} &= \frac{r}{x}
\end{align}
$$
**4.** $\left. \frac{\partial x}{\partial 4} \right|_{\theta}$
$$
\begin{align}
x &= r\cos\theta \\
\frac{\partial x}{\partial r} &= \cos\theta \\
\frac{\partial x}{\partial r} &= \frac{x}{r}
\end{align}
$$

**5.** $\left. \frac{\partial x}{\partial \theta} \right|_{y}$
$$
\begin{align}
x &= y\cot\theta \\
\frac{\partial x}{\partial \theta} &= -y\csc^2\theta \\
\frac{\partial x}{\partial \theta} &= -\frac{y}{(y/r)^2} \\
\frac{\partial x}{\partial \theta} &= -\frac{r^2}{y}
\end{align}
$$
**6.** $\left. \frac{\partial x}{\partial \theta} \right|_{r}$
$$
\begin{align}
x &= r\cos\theta \\
\frac{\partial x}{\partial \theta} &= -r\sin\theta \\
\frac{\partial x}{\partial \theta} &= -y
\end{align}
$$

**7.** $\left. \frac{\partial r}{\partial x} \right|_{y}$
$$
\begin{align}
r^2 &= x^2 + y^2 \\
2r \cdot \frac{\partial r}{\partial x} &= 2x \\
\frac{\partial r}{\partial x} &= \frac{x}{r}
\end{align}
$$

**8.** $\left. \frac{\partial r}{\partial x} \right|_{\theta}$
$$
\begin{align}
r &= x\sec\theta \\
\frac{\partial r}{\partial x} &= \sec\theta \\
\frac{\partial r}{\partial x} &= \frac{r}{x}
\end{align}
$$

**9.** $\left. \frac{\partial r}{\partial y} \right|_{x}$
$$
\begin{align}
r^2 &= x^2 + y^2 \\
2r \cdot \frac{\partial r}{\partial y} &= 2y \\
\frac{\partial r}{\partial y} &= \frac{y}{r}
\end{align}
$$

**10.** $\left. \frac{\partial r}{\partial y} \right|_{\theta}$
$$
\begin{align}
r &= y\csc\theta \\
\frac{\partial r}{\partial y} &= \csc\theta \\
\frac{\partial r}{\partial y} &= \frac{r}{y}
\end{align}
$$

**11.** $\left. \frac{\partial r}{\partial \theta} \right|_{x}$
$$
\begin{align}
r &= x\sec\theta \\
\frac{\partial r}{\partial \theta} &= x\sec\theta\tan\theta \\
\frac{\partial r}{\partial \theta} &= x \cdot \frac{r}{x} \cdot \frac{y}{x} \\
\frac{\partial r}{\partial \theta} &= \frac{ry}{x}
\end{align}
$$

**12.** $\left. \frac{\partial r}{\partial \theta} \right|_{y}$
$$
\begin{align}
r &= y\csc\theta \\
\frac{\partial r}{\partial \theta} &= -y\csc\theta\cot\theta \\
\frac{\partial r}{\partial \theta} &= -y \cdot \frac{r}{y} \cdot \frac{x}{y} \\
\frac{\partial r}{\partial \theta} &= -\frac{rx}{y}
\end{align}
$$
