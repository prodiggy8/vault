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
