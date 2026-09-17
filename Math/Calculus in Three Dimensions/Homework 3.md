---
tags:
type:
author:
description:
aliases:
date created: Thursday, September 17th 2026, 11:14:57 am
date modified: Thursday, September 17th 2026, 11:15:12 am
---
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
&=1-2\cos t + \cos^2 + \sin^2t \\
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
Provided $0 < t < 2\pi$.
$$
\begin{align}
N(t)&=\frac{\langle \frac{1}{2}\cos\left( \frac{t}{2} \right), -\frac{1}{2}\sin\left( \frac{t}{2} \right),0 \rangle}{\sqrt{ \left( \frac{1}{2} \right)^2\left( \cos^2\left( \frac{t}{2} \right) + \sin^2\left( \frac{t}{2} \right) \right) }}  \\
&=
\end{align}
$$

