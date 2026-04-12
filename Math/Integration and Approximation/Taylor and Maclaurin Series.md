---
course: "[[Integration and Approximation]]"
note: 5
---
#### Taylor Series

The sum of polynomials used to approximate a function in the neighborhood of a point. They can be used to:
- Evaluate integrals of the form $e^{-x^2}$
- Compute limits
- Compute the series representation of functions

$$f(x)=\sum_{n=0}^\infty \frac{f^{(n)}(a)}{n!}(x-a)^n$$
$$f(x)=f(a) + f'(a)(x-a) + \frac{f''(a)}{2!}(x-a)^2+\frac{f'''(a)}{3!}(x-a)^3+\dots$$

#### Maclaurin Series

If $a=0$, then we call the series a Maclaurin Series for $f(x)$.

$$f(x)=\sum_{n=0}^\infty \frac{f^{(n)}(0)}{n!}x^n$$
$$f(x)=f(0) + f'(0)x + \frac{f''(0)}{2!}x^2+\frac{f'''(0)}{3!}x^3+\dots$$

#### Condition

We define the *Taylor polynomial* to be $T_n(x)=\sum_{i=0}^n \frac{f^{(i)}(a)}{i!}(x-a)^i$ with degree at most $n$.

The *remainder* is defined to be, $R_n(x)=f(x)-T_n(x)$, the error between the function and the $n^{th}$ degree Taylor polynomial for a given $n$.

> **Theorem:**
> If $lim_{n \rightarrow \infty}R_n(x)=0$ for $|x-a|<R$, then $f(x)=\sum_{n=0}^\infty \frac{f^{(n)}(a)}{n!}(x-a)^n$ on $|x-a|<R$.

In most cases, it is difficult to calculate the exact value of $R_n(x)$. We find an upper bound instead:

> **Taylor's Inequality**
> $|R_{n}(x) \leq \frac{M}{(n+1)!}|x-a|^{n+1}$

##### Notable Series

- Maclaurin series of $cos(x)$ 
$$cos(x) = \sum_{n=0}^\infty \frac{(-1)^n x^{2n}}{(2n)!}$$
- Maclaurin series of $sin(x)$
$$sin(x)=\sum_{n=0}^\infty \frac{(-1)^{n+1} x^{2n+1}}{(2n+1)!}$$
- Taylor series of $e^x$ about $a$
$$\sum_{n=0}^{\infty} e^a \frac{x^n}{n!}$$
