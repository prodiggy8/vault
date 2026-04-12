---
course: "[[Integration and Approximation]]"
note: 2
---
Previous: [[Trigonometric Integrals]]
Next: [[Sequences and Series II]]
# Sequences

A sequence $(a_n)=(a_1, a_2, a_3, \ldots)$ is a function $f: \mathbb{N} \rightarrow (-\infty, \infty)$ where $a_1 = f(1)$, $a_2=f(2)$, and so on.

The limit of sequence converges if $a_n \rightarrow L$ as $n \rightarrow \infty$ for some real number $L$.

- Can't use L'Hôpital's unless we define a function such that for all $x \in \mathbb{N}$, $f(x) = a_x$

*Squeezing Theorem:* If $a_n \leq b_n \leq c_n$ for all $n$ and if $lim_{n \rightarrow \infty}a_n=L=lim_{n \rightarrow \infty}c_n$, then the sequence $(b_n)$ converges and has limit $L$.

- If exponential, raise to $e$ and take the natural logarithm to eliminate it.
$$a_n=(1+\frac{k}{n})^n=e^{n \cdot ln(1+\frac{k}{n})}$$
$$lim_{n \rightarrow \infty}a_n=e^{lim_{n \rightarrow \infty}{n \cdot ln(1 + \frac{k}{n})}}$$*Important Limit Laws*

1. For $p>0$ and $a_n>0$, $lim_{n \rightarrow \infty}a_n^p=(lim_{n \rightarrow \infty}a_n)^p$
2. If $lim_{n \rightarrow \infty}|a_n| = 0$, then $lim_{n \rightarrow \infty}a_n = 0$

##### Geometric Sequences

The general form of a geometric sequence is $a \cdot r^n = a, ar, ar^2, \ldots$, where $a$ and $r$ are fixed real numbers. We call $r$ the common ratio.

$$lim_{n \rightarrow \infty}r^n=\begin{cases}\text{0} & {-1 < r < 1} \\ \text{1} & {r=1} \\ \infty & {r > 1} \\ \text{DNE} & {r \leq -1} \end{cases}$$

A sequence $a_n$ is

1. *Bounded* if if there exists a constant $M > 0$ such that $|a_n| \leq M$ for all $n$.
2. *Monotonic increasing* if $a_n \leq a_{n+1}$ for all $n$.
3. *Monotonic decreasing* if $a_n \geq a_{n+1}$ for all $n$.

If a sequence is bounded and monotonic, then the sequence converges.

# Series

Given a sequence we want to make sense of the infinite sum $\sum_{k=1}^{\infty}a_k$.

#### Geometric Series Test

If $|r| < 1$, the geometric series $\sum_{k=0}^\infty ar^k$ converges and is equal to $\frac{a}{1-r}$, otherwise it diverges.

#### Divergence Test

If $\sum_{k=0}^\infty a_k$ converges, it must be the case that $lim_{k \rightarrow \infty}a_k=0$.

*Important:* if the limit is not $0$ then, the series diverges, but if the limit is $0$, <mark style="background: #ADCCFFA6;">it may or may not converge</mark>. Another test is needed to determine.

### Integral Test

Consider a function $f(x)$ that is continuous, positive, and decreasing on $[1, \infty)$. For each integer $n \geq 1$, set $f(n) = a_n$.

1. $\sum_{k=0}^\infty a_k$ diverges if and only if $\int_1^{\infty}f(x)dx$ diverges.
2. $\sum_{k=0}^\infty a_k$ converges if and only if $\int_1^{\infty}f(x)dx$ converges.

- In general, we only need $f(x)$ to be positive and decreasing on some interval of the form $[a, \infty)$, $a>0$.

- To check if the function is decreasing, we must find $f'(x)<0$.

### P-Series Test

$\sum_{k=0}^\infty \frac{1}{k^p}$ converges if and only if $p>1$.

### Comparison Tests

This works for series with non-negative terms only.

##### Direct Comparison Test

Given two series $\sum_{k=n_0}^\infty a_k$ and $\sum_{k=n_0}^\infty b_k$ are infinite series with *non-negative* terms. Assume that $0 \leq a_k \leq b_k$ for all $k\geq n_0$

1. If series b converges, then a converges.
2. If series a diverges, then b diverges.

##### Limit Comparison Test

Suppose that $a_n>0$ and $b_n>0$ for all $n \geq n_0$. Assume $L=lim_{n\rightarrow \infty}\frac{a_n}{b_n}$.

1. If $0 < L < \infty$, then either both series converge or both diverge.
2. If $L=0$ and b converges, then a converges.
3. If $L=\infty$ and b diverges, then a diverges.