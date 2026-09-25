---
tags:
  - calculus
type:
author:
description:
aliases:
date created: Thursday, September 24th 2026, 6:12:20 pm
date modified: Thursday, September 24th 2026, 6:12:22 pm
---
# 1.
## a)
Rhumb line: $\phi(t)=t$, $\theta=\theta(t)$
$$ \vec{p}(t) = (\sin t\cos\theta,\ \sin t\sin\theta,\ \cos t) $$
$$ \begin{aligned} x'(t) &= \cos t\cos\theta + \sin t\cdot(-\sin\theta)\cdot\theta' = \cos t\cos\theta - \sin t\sin\theta\,\theta' \\ y'(t) &= \cos t\sin\theta + \sin t\cdot\cos\theta\cdot\theta' = \cos t\sin\theta + \sin t\cos\theta\,\theta' \\ z'(t) &= -\sin t \end{aligned}
$$
$$ \vec{p}\,'(t) = \bigl(\cos t\cos\theta - \sin t\sin\theta\,\theta',\ \ \cos t\sin\theta + \sin t\cos\theta\,\theta',\ \ -\sin t\bigr). $$

Now length:
$$ \begin{aligned} (x')^2 &= \cos^2 t\cos^2\theta - 2\cos t\sin t\cos\theta\sin\theta\,\theta' + \sin^2 t\sin^2\theta\,(\theta')^2 \\ (y')^2 &= \cos^2 t\sin^2\theta + 2\cos t\sin t\sin\theta\cos\theta\,\theta' + \sin^2 t\cos^2\theta\,(\theta')^2 \\ (z')^2 &= \sin^2 t \end{aligned} $$
$$ \begin{aligned} |\vec{p}\,'|^2 &= \cos^2 t(\cos^2\theta + \sin^2\theta) + \sin^2 t\,(\theta')^2(\sin^2\theta + \cos^2\theta) + \sin^2 t \\ &= \cos^2 t + \sin^2 t\,(\theta')^2 + \sin^2 t \\ &= 1 + \sin^2 t\,(\theta')^2. \end{aligned} $$

Therefore 
$$ \vec{T}(t) = \frac{\vec{p}\,'(t)}{|\vec{p}\,'(t)|} = \frac{\bigl(\cos t\cos\theta - \sin t\sin\theta\,\theta',\ \ \cos t\sin\theta + \sin t\cos\theta\,\theta',\ \ -\sin t\bigr)}{\sqrt{1 + \sin^2 t\,(\theta')^2}}. $$
## b)
Line of latitude has $\theta(u) = u$ and $\phi(u) = \phi_0$ constant. Substituting into $x = \sin\phi\cos\theta$, $y = \sin\phi\sin\theta$, $z = \cos\phi$:
$$
\vec{q}(u) = \bigl(\sin\phi_0\cos u,\ \sin\phi_0\sin u,\ \cos\phi_0\bigr).
$$

Differentiate each component ($\sin\phi_0$ and $\cos\phi_0$ are constants):
$$
\begin{aligned}
x'(u) &= \sin\phi_0\cdot(-\sin u) = -\sin\phi_0\sin u \\
y'(u) &= \sin\phi_0\cdot\cos u = \sin\phi_0\cos u \\
z'(u) &= 0
\end{aligned}
$$
$$
\vec{q}\,'(u) = \bigl(-\sin\phi_0\sin u,\ \sin\phi_0\cos u,\ 0\bigr).
$$

Magnitude:
$$
|\vec{q}\,'|^2 = \sin^2\phi_0\sin^2 u + \sin^2\phi_0\cos^2 u + 0 = \sin^2\phi_0(\sin^2 u + \cos^2 u) = \sin^2\phi_0.
$$
Then
$$
\vec{L}(u) = \frac{\vec{q}\,'(u)}{|\vec{q}\,'(u)|}
= \frac{\bigl(-\sin\phi_0\sin u,\ \sin\phi_0\cos u,\ 0\bigr)}{\sin\phi_0}
= \bigl(-\sin u,\ \cos u,\ 0\bigr).
$$

## c)
At $t$ the rhumb line is at$\phi = t$, $\theta = \theta(t)$. Line of latitude through this point has $\phi_0 = t$. From b, its unit tangent there is
$$
\vec{L} = \bigl(-\sin\theta,\ \cos\theta,\ 0\bigr).
$$

Since $\vec{T}$ and $\vec{L}$ are unit vectors, $\cos\beta = \vec{T}\cdot\vec{L}$.
$$
\cos\beta = \frac{(-\sin\theta)(\cos t\cos\theta - \sin t\sin\theta\,\theta') + (\cos\theta)(\cos t\sin\theta + \sin t\cos\theta\,\theta') + (0)(-\sin t)}{\sqrt{1 + \sin^2 t\,(\theta')^2}}.
$$
Simplifying
$$
\begin{aligned}
&-\sin\theta\cos t\cos\theta + \sin t\sin^2\theta\,\theta' + \cos\theta\cos t\sin\theta + \sin t\cos^2\theta\,\theta' \\
&= \bigl(-\cos t\sin\theta\cos\theta + \cos t\sin\theta\cos\theta\bigr) + \sin t\,\theta'\bigl(\sin^2\theta + \cos^2\theta\bigr) \\
&= 0 + \sin t\,\theta'.
\end{aligned}
$$

Therefore
$$
\cos\beta = \frac{\sin t\,\theta'(t)}{\sqrt{1 + \sin^2 t\,(\theta'(t))^2}}.
$$
## d)
$\beta$ is constant so from c, with $w = \sin t\,\theta'(t)$, $$ \cos\beta = \frac{w}{\sqrt{1 + w^2}}$$$$
\cos^2\beta = \frac{w^2}{1 + w^2} \implies \cos^2\beta\,(1 + w^2) = w^2 \implies \cos^2\beta = w^2 - w^2\cos^2\beta = w^2(1 - \cos^2\beta) = w^2\sin^2\beta
$$Hence:
$$
w^2 = \frac{\cos^2\beta}{\sin^2\beta} = \cot^2\beta \implies w = \pm\cot\beta
$$The denominator is positive, so $w$ and $\cos\beta$ have the same sign, and $\cot\beta$ has the same sign as $\cos\beta$. So $w$ and  $\cot\beta$ have the same sign, $w=\cot \beta$.
$$ \sin t\,\theta'(t) = \cot\beta \implies \theta'(t) = \frac{\cot\beta}{\sin t}. $$
## e)
From d, $\theta'(t) = \dfrac{\cot\beta}{\sin t}$, so $$ \theta(t) = \cot\beta\int\frac{dt}{\sin t}. $$ $$
\frac{1}{\sin t} = \frac{1}{2\sin(t/2)\cos(t/2)} = \frac{1}{2\sin(t/2)\cos(t/2)}\cdot\frac{\cos(t/2)}{\cos(t/2)} = \frac{\tfrac{1}{2}\sec^2(t/2)}{\tan(t/2)}
$$
Substitution: $u = \tan(t/2)$, $du = \tfrac{1}{2}\sec^2(t/2)\,dt$. Then 
$$ 
\int\frac{dt}{\sin t} = \int\frac{du}{u} = \log|u| + C = \log\tan(t/2) + C
$$  Therefore: $$ \theta(t) = \cot(\beta)\log\tan(t/2) + C. $$
## f)
$$
s = \int_{t_0}^{t_1}|\vec{p}\,'(t)|\,dt.
$$
$|\vec{p}\,'(t)| = \sqrt{1 + \sin^2 t\,(\theta')^2}$ from first part. Then $\sin t\,\theta' = \cot\beta$, so
$$
|\vec{p}\,'(t)| = \sqrt{1 + \cot^2\beta} = \sqrt{\csc^2\beta} = \csc\beta
$$
So:
$$
s = \int_{t_0}^{t_1}\csc\beta\,dt = \csc\beta\,(t_1 - t_0)
$$

## g)
The Mercator map is $(\theta, \phi) \mapsto (x, y) = \bigl(\theta,\ \log\tan(\phi/2)\bigr)$.

On the rhumb line, $\phi = t$ and $\theta = \cot(\beta)\log\tan(t/2) + C$, so
$$
x = \cot(\beta)\log\tan(t/2) + C, \qquad y = \log\tan(t/2).
$$

So:
$$
x = \cot(\beta)\,y + C.
$$

Rewriting as $y = \tan(\beta)(x - C)$this is a straight line. Lines of latitude map to horizontal lines, so the rhumb line still crosses them at angle $\beta$ on the map.

Near the pole $\tan \frac{t}{2}$ tends to 0 so $y$ becomes so the poles are pushed off to infinity (log) and everything near them is stretched.

# 2.

## a)
$r(t)=t$, $\theta(t)=\theta_{0}$ where $t \geq 0$ and $\theta_{0}$ is a constant.
$\hat{r}(r,\theta)$ tangent at $P$ whose coordinates are $r, \theta$

$x(t)=r(t)\cos \theta=t\cos \theta_{0}$
$y(t) = r(t)\sin \theta=t\sin \theta_{0}$

$x'(t)=\cos \theta_{0}$
$y'(t)=\sin \theta_{0}$

Tangent: $y=$$\tan \theta_{0}\cdot x$

## b)
$\hat{\theta}(r,\theta)$ with $r(t)=r_{0}$ and $\theta(t)=t$

$x(t)=r(t)\cos \theta(t)=r_{0}\cos t$
$y(t) = r(t)\sin \theta(t)=r_{0}\sin t$

$x'(t)=-r_{0}\sin t$
$y'(t)=r_{0}\cos t$

Tangent: 
$y-r_{0}\sin t=-\cot t \cdot (x-r_{0}\cos t)$
$y=-\cot t \cdot x + r_{0}(\cot t \cos t + \sin t)$
$y=-\cot t \cdot x + r_{0}\left( \frac{\cos^2t}{\sin t} + \sin t \right)$
$y=-\cot t \cdot x + r_{0}\left( \frac{\cos^2t + \sin^2t}{\sin t} \right)=-\cot t \cdot x + \frac{r_{0}}{\sin t}$

## c)
In Cartesian:
$p(t)=(t\cos \theta_{0},t\sin \theta_{0})$
$p’(t)=(\cos \theta_{0},\sin \theta_{0})$ of length $1$ so already unit.
$\hat{r}=(\cos \theta,\sin \theta)$

$p(t)=(r_{0}\cos t, r_{0}\sin t)$
$p'(t)=(-r_{0}\sin t,r_{0}\cos t)$ of length $r_{0}$ so:
$p'(t)=(-\sin t, \cos t)$ unit
$\hat{\theta}=(-\sin \theta,\cos \theta)$

$\hat{r} \cdot \hat{\theta}=(\cos \theta)(-\sin \theta)+\sin \theta \cos \theta=0$
Hence they are orthogonal.

## d)
$\hat{r}=\cos \theta \hat{x} + \sin \theta \hat{y}$
$\hat{\theta}=-\sin \theta \hat{x} + \cos \theta \hat{y}$


$\hat{r} \cos \theta=\cos^2\theta \hat{x} + \sin \theta \cos \theta \hat{y}$
$\hat{\theta} \sin \theta=-\sin^2 \hat{x}+\sin \theta \cos \theta \hat{y}$
$\cos \theta \hat{r}-\sin \theta \hat{\theta}=(\cos^2+\sin^2)\hat{x}$
$\hat{x}=\hat{r}\cos \theta- \hat{\theta}\sin \theta$

$\hat{r} \sin \theta=\cos \theta \sin \theta \hat{x} + \sin^2 \theta \hat{y}$
$\hat{\theta}\cos \theta=-\sin \theta \cos \theta \hat{x} + \cos^2\theta \hat{y}$
$\sin \theta \hat{r} + \cos \theta \hat{\theta}=(\sin^2 \theta + \cos^2 \theta)\hat{y}$
$\hat{y}=\sin \theta \hat{r}+\cos \theta \hat{\theta}$

## e)
$\hat{r}(t) = \cos\theta(t)\,\hat{x} + \sin\theta(t)\,\hat{y}$
$\hat{\theta}(t) = -\sin\theta(t)\,\hat{x} + \cos\theta(t)\,\hat{y}$

$$
\begin{aligned}
\hat{r}'(t) &= -\sin\theta \cdot \theta'\,\hat{x} + \cos\theta \cdot \theta'\,\hat{y} \\
&= \theta'\left(-\sin\theta\,\hat{x} + \cos\theta\,\hat{y}\right) \\
&= \theta'(t)\,\hat{\theta}(t)
\end{aligned}
$$
$$
\begin{aligned}
\hat{\theta}'(t) &= -\cos\theta \cdot \theta'\,\hat{x} - \sin\theta \cdot \theta'\,\hat{y} \\
&= -\theta'\left(\cos\theta\,\hat{x} + \sin\theta\,\hat{y}\right) \\
&= -\theta'(t)\,\hat{r}(t)
\end{aligned}
$$
$$
\hat{r}' = \theta'\hat{\theta}, \qquad \hat{\theta}' = -\theta' \hat{r}
$$
## f)
$\vec{r}(t) = r(t)\,\hat{r}(t)$ so by product rule:
$$
\vec{r}\,'(t) = r'(t)\,\hat{r}(t) + r(t)\,\hat{r}\,'(t).
$$
Since $\hat{r}(t) = \cos\theta(t)\,\hat{x} + \sin\theta(t)\,\hat{y}$ with $\hat{x}, \hat{y}$ constant,
$$
\hat{r}\,'(t) = \theta'(t)\left(-\sin\theta\,\hat{x} + \cos\theta\,\hat{y}\right) = \theta'(t)\,\hat{\theta}(t).
$$
Therefore
$$
\vec{r}\,'(t) = r'(t)\,\hat{r} + r(t)\,\theta'(t)\,\hat{\theta}.
$$

## g)
From before: $$ \vec{r}\,'(t) = r'(t)\,\hat{r} + r(t)\theta'(t)\,\hat{\theta}, \qquad \hat{r}\,'(t) = \theta'(t)\,\hat{\theta}, \qquad \hat{\theta}\,'(t) = -\theta'(t)\,\hat{r}. $$we do product rule: 
$$ \bigl(r'(t)\,\hat{r}\bigr)' = r''(t)\,\hat{r} + r'(t)\,\hat{r}\,'(t) = r''(t)\,\hat{r} + r'(t)\theta'(t)\,\hat{\theta}.
$$
$$ \bigl(r(t)\theta'(t)\,\hat{\theta}\bigr)' = r'(t)\theta'(t)\,\hat{\theta} + r(t)\theta''(t)\,\hat{\theta} + r(t)\theta'(t)\,\hat{\theta}\,'(t)
$$
$$= r'(t)\theta'(t)\,\hat{\theta} + r(t)\theta''(t)\,\hat{\theta} - r(t)(\theta'(t))^2\,\hat{r}$$
Hence, adding and collecting like terms:
$$ \vec{r}\,''(t) = \bigl(r''(t) - r(t)(\theta'(t))^2\bigr)\,\hat{r} + \bigl(2r'(t)\theta'(t) + r(t)\theta''(t)\bigr)\,\hat{\theta}. $$
# 3.
Since the ratio does not depend on the shape, take $D$ to be a triangle. Place one vertex at the origin (translation does not change areas or the projection), and let the other two vertices be $\vec{a} = (a_1, a_2, a_3)$ and $\vec{b} = (b_1, b_2, b_3)$. Then
$$
\text{Area}(D) = \tfrac{1}{2}\,|\vec{a}\times\vec{b}|.
$$
Since $\vec{a}\times\vec{b}$ is normal to the plane of $D$, $\vec{a}\times\vec{b} = \pm|\vec{a}\times\vec{b}|\,\hat{u}$.

Projecting to the $xy$-plane sets the $z$-component to zero: $\vec{a}\,' = (a_1, a_2, 0)$, $\vec{b}\,' = (b_1, b_2, 0)$. The projected triangle $D'$ has area
$$
\text{Area}(D') = \tfrac{1}{2}\,|\vec{a}\,'\times\vec{b}\,'| = \tfrac{1}{2}\,|a_1 b_2 - a_2 b_1|.
$$
But $a_1 b_2 - a_2 b_1$ is exactly the $z$-component of $\vec{a}\times\vec{b}$, so
$$
\text{Area}(D') = \tfrac{1}{2}\,\left|(\vec{a}\times\vec{b})\cdot\hat{z}\right| = \tfrac{1}{2}\,|\vec{a}\times\vec{b}|\,|\hat{u}\cdot\hat{z}| = \text{Area}(D)\,|\hat{u}\cdot\hat{z}|.
$$

Therefore
$$
\frac{\text{Area}(D)}{\text{Area}(D')} = \frac{1}{|\hat{u}\cdot\hat{z}|} = \frac{1}{|\cos\varphi|},
$$
where $\varphi$ is the angle between $\hat{u}$ and $\hat{z}$. If $\hat{u} = (u_1, u_2, u_3)$, this is $1/|u_3|$.