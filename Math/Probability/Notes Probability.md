This is y15-24
3.4-3.6
4.1-4.3
5.1-5.5
6.1

Chapter 3
PDF properties
- all values greater than 0
- sum to 1

for Y = aX + b
	E[Y] = aE[X] + b
	var(Y) = a^2 * var(X)

For uniform: 
mean: a + b / 2
variance: (b - a)^2 / 12

CDF

Fx(x) = P(X <= x) = Integral from -inf to x fx(t) dt

- review normal random variable and table!

JOINT PDFS OF MULTIPLE RANDOM VARIABLES

Joint PDF 
If B (the event of interest) is a rectangle, we have:
$$P(a \le X \le b, c \le Y \le d) = \int_c^d \int_a^b f_{X,Y}(x, y) dx dy$$
By normalization, we must have:
$$\int_{-\infty}^{\infty}f_{X,Y}(x, y)dxdy=1$$
Obtain marginal PDF from joint PDF:
$$f_X(x)=\int_{-\infty}^{\infty}f_{X,Y}(x, y)dy$$
$$f_Y(y)=\int_{-\infty}^{\infty}f_{X,Y}(x, y)dx$$
To fix ranges, we need to know what values y or x can assume.

**CDF**
$$\int_{-\infty}^x \int_{-\infty}^y f_{X,Y}(s, t) dt ds$$

Let Z be a random variable given by $g(X,Y)$. Method to get the PDF of Z will be given on section **4.1**. But expectation:
$$\mathbb{E}[g(X, Y)]=\int_{-\infty}^{\infty}\int_{-\infty}^{\infty}g(x, y)f_{X,Y}(x, y) dx dy$$

**Conditioning of Continuous Random Variables** (16, 3.5)

The **conditional PDF** of a variable is defined as a function:
$$P(X \in B | A)= \int_Bf_{X|A}(x)dx$$
Special case: if condition is of the form $X \in A$
$$P(x \in B | x \in A) = \frac{P(x \in B, x \in A)}{P(x \in A)}=\frac{\int_{A \cap B}f_X(x)dx}{P(x \in A)}$$**Conditional PDF**
$$f_{X|A}(x)=\frac{f_X(x)}{P(x \in A)} \text{ if } x \in A$$
Given that A is an event.

**Conditioning to another variable**
