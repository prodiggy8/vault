---
tags:
  - computational-perception
  - perception
  - computer-science
type: note
author:
description:
aliases:
date created: Sunday, October 4th 2026, 1:01:39 pm
date modified: Sunday, October 4th 2026, 1:01:46 pm
---
We can model a neuron as weighted sum of light falling on its receptive field, with weights $w$:
$$r=\sum_{m,n}w(m,n)I(m,n)$$
That is a dot product between the filter and the image patch.

> [!Convolution]
> The convolution of image $f$ with filter (“kernel”) $h$ is 
> $$(f * h)(x) = \sum_{k}f(x-k)h(k)$$
> We reverse $h$, slide to position $x$, multiply overlapping entries, and add. For symmetric filters (Gaussians) flipping does nothing.
> 
> For 2D signals:
> $$(I * h)(x, y) = \sum_{m,n}I(x-m, y-n)h(m,n)$$

A 1D Gaussian with standard deviation $\sigma$ is:
$$G_{\sigma}(x)=\frac{1}{\sqrt{ 2\pi } \sigma}e^\frac{-x^2}{2\sigma^2}$$
In 2D it is:
$$G_{\sigma}(x,x)=G_{\sigma}(x)G_{\sigma}(y)=\frac{1}{\sqrt{ 2\pi }\sigma}e^\frac{-(x^2+y^2)}{2\sigma^2}$$
It blurs but does not change the average brightness. Larger $\sigma$ means wider bell and more blur. Since it factors into two separate Gaussians you can do a horizontal then a vertical.

Smoothing removes fine detail and noise, and selects a scale: after blurring you only see structure bigger than about $\sigma$.

### Center-surround as DoG

We can model a ganglion cell as excitation from center minus inhibition from horizontal cells from a wider region as $\operatorname{DoG}(x,y)=G_{\sigma_{1}}(x,y)-G_{\sigma_{2}}(x,y)$. This is the **Mexican hat**.

Fits to real ganglion cells give $\frac{\sigma_{2}}{\sigma_{1}}=1.75$ (Wilson & Bergen, 1979).

Filtering with it, since convolution is linear: $I * \operatorname{DoG}(x,y)=I * G_{\sigma_{1}}-I * G_{\sigma_{2}}$

### The Laplacian of Gaussian

> [!Laplacian]
> On a pixel grid, derivatives are differences.
> $$\begin{align}
> f'(x) &\approx f(x+1) - f(x) &\text{filter } &\left[-1,1\right] \\
> f''(x) &\approx f'(x) - f'(x-1) = f(x+1) - 2f(x) + f(x-1) &\text{filter } &\left[1,-2, 1\right]
> \end{align}$$
> The second derivative measures curvature: how much $f(x)$ differs from the average of its neighbors. In 2D the **Laplacian** adds the second derivatives in both directions:
> $$
> \begin{align}
> \Delta^2f=\dfrac{\partial^2f}{\partial x^2} + \dfrac{\partial^2f}{\partial y^2} && \begin{bmatrix}
> 0 & 1 & 0 \\
> 1 & -4 & 1 \\
> 0 & 1 & 0
> \end{bmatrix}
> \end{align}
> $$

Derivatives amplify noise so Marr suggested to smooth with Gaussian then apply the derivative. An ON-center cell corresponds to:
$$(-\Delta^2G\sigma) * I$$
**DoG approximate LoG** (nature doesn’t do derivatives)
The best approximation for it using DoG is $1.6$.

Since spikes fired by ganglion cells are **always positive**, we must have **two types of cell:** ON-center and OFF-center.
$$
\begin{align}
\text{ON} = \max(0,x) && \text{OFF} = \max(0, -x)
\end{align}
$$
This is ReLU from deep learning.


## Summary
- A neuron’s response is modelled as a dot product of its receptive field with the image. Doing this at every position is convolution.
- The center-surround is a DoG $\approx$ negated Laplacian of Gaussian.
- ON and OFF channels are the ReLU of that signed signal.

