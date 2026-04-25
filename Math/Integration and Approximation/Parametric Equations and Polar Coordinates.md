---
course: "[[Integration and Approximation]]"
note: 6
---

#### Parametric Equations

Instead of defining $y$ in terms of $x$ or $x$ in terms of $y$, we can define both $x$ and $y$ in terms of a third variable called a parameter as follows,
$$x=f(t) \qquad y=g(t)$$
The graph of all $(x, y)$ is called the *parametric curve*.

Sketching:
1. Point-by-point
2. Eliminating a parameter

**Area:** given a curve $C$ described by $x=f(t)$ and $y=g(t)$ for $a\leq t \leq b$  where $y>0$ on $[a,b]$ and $C$ is traced exactly once as $t$ increases from $a$ to $b$, then:
$$A=\int_{a}^{b} g(t)f'(t) dt $$
**Arc Length:** given a curve $C$ described by $x=f(t)$ and $y=g(t)$ for $a\leq t \leq b$  where $f'$, $g'$ are continuous on $[a,b]$ and $C$ is traced exactly once as $t$ increases from $a$ to $b$, then the length $L$ of $C$ is given by:
$$L= \int^{b}_{a} \sqrt{ (\frac{dx}{dt})^2 + (\frac{dy}{dt})^2 \; dt}$$
#### Polar Coordinates