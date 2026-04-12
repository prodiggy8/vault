---
course: "[[Integration and Approximation]]"
note: 4
---
Previous : [[Sequences and Series II]]
Next: [[Taylor and Maclaurin Series]]
# Power Series

A power series is any series that can be written in the form:
$$\sum_{n=0}^\infty c_n(x-a)^n$$
A power series is a function of x and it may converge for some values of x.

There is a number $R$ so that the *power series will converge for* $|x-a|<R$. This number is called the **radius of convergence** for the series.

The **interval of convergence** is the interval of all values of x for which the series converges.

The interval of convergence must contain $a-R < x < a+R$. 
We need to manually check if $x=a-R$ and $x=a+R$ are also in the interval.

$x=a$ is **guaranteed to converge** in a power series.

## Power Series and Functions

Geometric series is $\sum_{n=1}^\infty ar^n=\frac{a}{1-r}$, given $|r|<1$.
If $a=1$ and $r=x$ then, $\sum_{n=1}^\infty x^n=\frac{1}{1-x}$, given $|x|<1$.

##### Lecture notes

Given $f(x)=\sum_{n=1}^\infty c_k(x-a)^k=c_0+c_1(x-a)+c_2(x-a)+\dots$, then $f(x)$ is continuous and differentiable on the interval $(a-R,a+R)$.

- $f'(x)=c_1+2c_2(x-a)+3c_3(x-a)^2+\dots=\sum_{n=1}^\infty kc_k(x-a)^{k-1}$
- $\int f(x)=C+c_0(x-a)+\frac{c_1(x-a)^2}{2}+\dots=C+\sum_{k=1}^\infty \frac{c_k(x-a)^{k+1}}{k+1}$

The interval of convergence **does not change**.