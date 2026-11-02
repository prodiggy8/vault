### Problem 1
$$
\begin{align}
x^2 + y^2 = x + y + 2  \\
x^2 - x + y^2 - y = 2 \\
\left(x^2 - x + \tfrac14\right) + \left(y^2 - y + \tfrac14\right) = 2 + \tfrac14 + \tfrac14 \\
\left(x - \tfrac{1}{2}\right)^2 + \left(y - \tfrac{1}{2}\right)^2 = \tfrac{5}{2}
\end{align}
$$

So the projection onto the $xy$-plane is a disk $D$ centered at $\left(\tfrac12, \tfrac12\right)$ with radius $R = \sqrt{5/2}$.

$$ V = \iint_D \left[(x + y + 2) - (x^2 + y^2)\right] dA = \iint_D \left[\tfrac{5}{2} - \left(x - \tfrac12\right)^2 - \left(y - \tfrac12\right)^2\right] dA $$

Using: $x - \tfrac12 = r\cos\theta, \; y - \tfrac12 = r\sin\theta$.

$$ V = \int_0^{2\pi} \int_0^{\sqrt{5/2}} \left(\tfrac{5}{2} - r^2\right) r , dr , d\theta $$
$$ = 2\pi \left[\tfrac{5}{4} r^2 - \tfrac{1}{4} r^4\right]_0^{\sqrt{5/2}} = 2\pi \left(\tfrac{25}{8} - \tfrac{25}{16}\right) = 2\pi \cdot \tfrac{25}{16} = \frac{25\pi}{8} $$

### Problem 2

Centering sphere at  origin with  hole along $z$-axis. At height $z$, it’s a disk of radius $\sqrt{R^2 - z^2}$ with a disk of radius $a$ removed, so with $h = \sqrt{R^2 - a^2}$
$$A(z) = \pi\left(R^2 - z^2 - a^2\right) = \pi\left(h^2 - z^2\right), \qquad -h \le z \le h$$ $$V = \int_{-h}^{h} \pi\left(h^2 - z^2\right) dz = \pi\left(2h^3 - \tfrac{2}{3}h^3\right) = \frac{4\pi}{3}h^3 = \frac{4\pi}{3}\left(R^2 - a^2\right)^{3/2}$$
### Problem 3
##### a)
Since letter used for the variable of integration doesn't affect the value of a definite integral:
$$I^2 = \left(\int_{-\infty}^{\infty} e^{-x^2} \, dx\right)\left(\int_{-\infty}^{\infty} e^{-y^2} \, dy\right)$$

The first integral is a constant with respect to $y$, so it can be moved inside the second:

$$  
I^2 = \int_{-\infty}^{\infty} \left(\int_{-\infty}^{\infty} e^{-x^2} \, dx\right) e^{-y^2} \, dy  
= \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} e^{-x^2} e^{-y^2} \, dx \, dy  
= \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} e^{-x^2 - y^2} \, dx \, dy  
$$

Integrating over every $x$ and then over every $y$ covers the whole plane, so:
$$I^2 = \iint_{\mathbb{R}^2} e^{-x^2 - y^2} \, dA$$
##### b)
 $$
 \begin{align}
 x^2 + y^2 = r^2 \\
 dA = r \, dr \, d\theta \\
 0 \le r < \infty \\
 0 \le \theta \le 2\pi
 \end{align}
$$
$$
I^2 = \int_0^{2\pi} \int_0^{\infty} e^{-r^2} r \, dr \, d\theta  
= 2\pi \left[-\tfrac{1}{2} e^{-r^2}\right]_0^{\infty}  
= 2\pi \cdot \tfrac{1}{2}  
= \pi  
$$
$$I = \sqrt{\pi}$$
##### c)
Since $e^{-u^2}$ is even:
$$\int_0^{\infty} e^{-u^2} \, du = \frac{\sqrt{\pi}}{2}$$
Let $x = u^2$, $dx = 2u \, du$:

$$\int_0^{\infty} x^{-1/2} e^{-x} \, dx = \int_0^{\infty} u^{-1} e^{-u^2} \, 2u \, du = 2 \int_0^{\infty} e^{-u^2} \, du = \sqrt{\pi}$$

For the second integral, we integrate by parts:
$$u = x^{1/2}, \quad du = \tfrac{1}{2} x^{-1/2} \, dx, \qquad dv = e^{-x} \, dx, \quad v = -e^{-x}$$
$$\int_0^{\infty} x^{1/2} e^{-x} \, dx = \left[-x^{1/2} e^{-x}\right]_0^{\infty} + \frac{1}{2} \int_0^{\infty} x^{-1/2} e^{-x} \, dx = 0 + \frac{1}{2}\sqrt{\pi} = \frac{\sqrt{\pi}}{2}$$
### Problem 4
Set coords so center of mass is at origin and $\hat{u}$ points along $z$-axis. et $\rho(x, y, z)$ be the density, so:
$$m = \iiint_R \rho \, dV$$
Because the center of mass is at the origin:

$$\iiint_R x \rho \, dV = 0, \qquad \iiint_R y \rho \, dV = 0$$

The axis through the center of mass is the $z$-axis. A point $(x, y, z)$ is at distance $\sqrt{x^2 + y^2}$ from it, so:
$$I_{\text{cm}} = \iiint_R \left(x^2 + y^2\right) \rho \, dV$$
The parallel axis is the vertical line through $(a, b, 0)$, where $a^2 + b^2 = d^2$. A point $(x, y, z)$ is at distance $\sqrt{(x - a)^2 + (y - b)^2}$ from it, so:
$$I = \iiint_R \left[(x - a)^2 + (y - b)^2\right] \rho \, dV$$
Expand the squares:

$$(x - a)^2 + (y - b)^2 = \left(x^2 + y^2\right) - 2ax - 2by + \left(a^2 + b^2\right)$$

Split the integral into four pieces:

$$I = \iiint_R \left(x^2 + y^2\right) \rho \, dV - 2a \iiint_R x \rho \, dV - 2b \iiint_R y \rho \, dV + \left(a^2 + b^2\right) \iiint_R \rho \, dV$$

The first piece is $I_{\text{cm}}$, the middle two are $0$, and the last is $d^2 m$. Hence:
$$I = I_{\text{cm}} - 0 - 0 + m d^2 = I_{\text{cm}} + m d^2$$