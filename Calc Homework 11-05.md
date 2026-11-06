---
tags:
type:
author:
description:
aliases:
date created: Thursday, November 5th 2026, 8:57:23 pm
date modified: Thursday, November 5th 2026, 8:57:32 pm
---
### Problem 1
**1.**
Change variables to: $u = PV$ and $w = PV^\gamma$
Then the region becomes the rectangle $T_1 \le u \le T_2$, $a \le w \le b$.

The map is one-to-one, since $w/u = V^{\gamma-1}$ gives $V = (w/u)^{1/(\gamma-1)}$ and then $P = u/V$.

Jacobian:

$$\frac{\partial(u,w)}{\partial(P,V)} = \begin{vmatrix} V & P \\ V^\gamma & \gamma P V^{\gamma-1} \end{vmatrix} = \gamma P V^\gamma - P V^\gamma = (\gamma-1)PV^\gamma = (\gamma - 1)w$$

So $dP\,dV = \dfrac{du\,dw}{(\gamma-1)w}$, and area is:
$$\begin{aligned} A &= \int_{T_1}^{T_2}\int_a^b \frac{1}{(\gamma-1)w}\,dw\,du \\  
&= \frac{1}{\gamma-1}\int_{T_1}^{T_2}\Big[\log w\Big]_a^b\,du \\  
&= \frac{1}{\gamma-1}\int_{T_1}^{T_2}(\log b - \log a)\,du \\  
&= \frac{1}{\gamma-1}\log\frac ba\,\Big[u\Big]_{T_1}^{T_2} \\  
&= \frac{1}{\gamma-1}(T_2 - T_1)\log\frac{b}{a}.  
\end{aligned}  
$$

