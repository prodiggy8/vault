##### Multiplication

**Lattice**

Given a pair of arrays $X[0 \dots m-1]$ and  $Y[0 \dots n-1]$ such that
$$x=\sum_{i=0}^{m-1}X[i] \cdot 10^i \;\;\;\;\;\; y=\sum_{j=0}^{n-1}Y[j] \cdot 10^j$$ The algorithm follows
$$x\cdot y= \sum_{i=0}^{m-1} \sum_{j=0}^{n-1} (X[i] \cdot Y[j] \cdot 10^{i+j})$$

Runs in $O(mn)$.

**Peasant**

```pseudocode title:PeasantMultiply(x,y):
prod = 0
while x > 0
	if x is odd
		prod = prod + y
	x = x / 2
	y = y + y
return prod
```

Or, more simply

$$x \cdot y = \begin{cases}\left\lfloor {\frac{x}{2}}   \right\rfloor \cdot (y+y) && \text{if } x \text{ is even} \\ \left\lfloor {\frac{x}{2}}   \right\rfloor \cdot (y+y) + y && \text{if } x \text{ is odd} \end{cases}$$
This is a recursive algorithm.
And it runs in $O(mn)$ time as well.
