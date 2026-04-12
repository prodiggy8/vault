$a=qn+r$, where $r$ is the rest
$a \equiv b \mod{n}$ means $n | b-a$ or even $rem(a, n) = rem(b, n)$
This partitions $\mathbb{Z}$ in n equivalence classes from $0$ to $n-1$
$a \equiv_n b \Rightarrow a+x \equiv_n b+x$ and $ax \equiv_n bx$

Each row and column of $+_n$ is a permutation of $\mathbb{Z}_n$
$-a=x$ if and only if $a + x \equiv_n 0$
$a -_n b$ requires finding $-b$ and then $a + (-b)$

**Theorem:** There are exactly $\frac{n}{gcd(a, n)}$ multiples of $a \mod n$
Row $a$ has permutation property $\Leftrightarrow gcd(a, n) = 1$

**Theorem:** $ax \equiv_n ay \Rightarrow x \equiv_{\frac{n}{gcd(a, n)}} y$

$\mathbb{Z}^*_n=\{a \in \{0, 1, ..., n-1\} \mid gcd(a, n) = 1\}$
$\phi(n)=|\mathbb{Z}_n^*|$

$\text{n prime} \Rightarrow \phi(n)=n-1$
$\text{p, q distinct primes} \Rightarrow \phi(pq)=(p-1)(q-1)$

Inverse of $a$ exists if by Euclidean algorithm $gcd(a, n) = 1$
Finding such inverse requires writing $1$ as a linear combination of $a$ and $n$

**Exponentiation**
1. Square and mod intermediate results if exponent is power of 2
2. Store intermediate powers (represent exponent in binary) and multiply mod

If $a$ is super large, we substitute by $rem(a, n)$
If $b$ is super large, we substitute by $rem(b, \phi(n))$

**Euclidean algorithm**
1. Start dividing $n$ by $a$
2. Then divide $a$ by the rest of the previous step

**Diophantine equations**
$ax + by = c$
Solution exists $\Leftrightarrow d=gcd(a, b) \mid c$

1. Divide $a$, $b$, and $c$ by $gcd(a, b)$
2. Find $x_0$ and $y_0$ with the Extended Euclidean Algorithm
3. Multiply them by $\frac{c}{d}$
4. $x=x_0 + k \cdot \frac{b}{d}$ and $y=y_0-k \cdot \frac{a}{d}$

**Euler's Theorem:** $a \in \mathbb{Z}_n^* \Rightarrow a^{phi(n)} \equiv_n 1$
**Fermat's Little Theorem:** If $n$ is prime and $1 \le a \le n-1$, then $a^{n-1} \equiv_n 1$
