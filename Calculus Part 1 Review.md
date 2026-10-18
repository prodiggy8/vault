---
tags:
  - calculus
type:
author:
description:
aliases:
date created: Sunday, October 18th 2026, 5:19:52 pm
date modified: Sunday, October 18th 2026, 5:19:58 pm
---
# 2.3
$$
u \cdot v = |u||v| \cos \theta
$$
If **orthogonal**: $u \cdot v = 0$
If **parallel**:
$$
\begin{align}
u &= cv \\
u \cdot v &= \pm|u||v|
\end{align}
$$
### Projections
$$\operatorname{proj}_{u}v=\frac{u \cdot v}{|u|^2} \hat{u}$$
Is the component of $v$ in the **direction of $u$**

Example of use:
- Want to change basis of $u$ to be $v$ and $w$ such that $v \perp w$
$$u=\operatorname{proj}_{v}u + \operatorname{proj}_{w}u$$
- Suppose we only have one vector $v$ and need to find $w$
$$u = \operatorname{proj}_{v}u + (u - \operatorname{proj}_{v}u)$$

# 2.4
