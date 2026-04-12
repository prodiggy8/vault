---
course: "[[Integration and Approximation]]"
note: 3
---
### 11.5. Alternating Series and Absolute Convergence

Alternating series: terms are alternately positive and negative.

*Alternating Series Test*

If series $\sum_{n=1}^\infty (-1)^{n-1}a_n$ with $a_n$ positive, satisfies:

1. $0 < a_{n+1} \leq a_n$ for all $n \geq n_0$ for some integer $n_0$
2. $lim_{n \rightarrow \infty} a_n = 0$

then the series is convergent.

To remember:
- $\frac{d}{dx} a^x = a^x \; ln \; a$
- $\frac{d}{dx} a^u = a^u \; ln \; a \; \frac{du}{dx}$

**Absolute and Conditional Convergence**

The series $\sum_{k=1}^\infty \frac{sin \; k}{k^2}$ has positive and negative terms but it's not an alternating series.

*The Absolute Convergence Test*

If $\sum_{k=1}^\infty |a_k|$ converges, then $\sum_{k=1}^\infty a_k$ converges.

- The converse is not true in general.

An **absolutely convergent** series means $\sum_{k=1}^\infty |a_k|$ converges.
A **conditionally convergent** series means $\sum_{k=1}^\infty |a_k|$ does not converge, but $\sum_{k=1}^\infty a_k$ does.
### 11.6. The Ratio and Root Tests

*Ratio Test*

Assume that $\sum_{k=1}^\infty a_k$ is a series with positive terms and let $r=lim_{n \rightarrow \infty}\frac{a_{n+1}}{a_n}$.

1. If $r < 1$, the series converges.
2. If $r>1$, the series diverges.
3. If $r=1$, the test is inconclusive.

To remember:
- $(\frac{n+1}{n})^n=(1+\frac{1}{n})^n = e$
- $(\frac{n}{n+1})^n=\frac{1}{(\frac{n+1}{n})^n}=\frac{1}{e}$
- $(1+\frac{k}{n})^n=e^k$

**When to use:** factorials, exponentials

*The Root Test*

Assume that $\sum_{k=1}^\infty a_k$ is a series with positive terms and let $r=lim_{n \rightarrow \infty}\sqrt[n]{a_n}$.

1. If $r<1$, the series converges.
2. If $r>1$, the series diverges.
3. If $r=1$, the test is inconclusive.

To remember:
- $lim_{x \rightarrow \infty} \sqrt[x]{x}=1$

**When to use:** entire term to $n$-th power, exponentials

