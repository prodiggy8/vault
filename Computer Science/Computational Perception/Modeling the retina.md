---
tags:
type:
author:
description:
aliases:
date created: Monday, September 21st 2026, 10:01:51 am
date modified: Monday, September 21st 2026, 10:02:04 am
---
The retina doesn’t represent an image as luminance.
- 100 million photoreceptors for 1 million retinal ganglion cells; some information must be discarded.
- Natural images are redundant; neighboring pixels are strongly correlated. Subtracting local prediction removes the redundancy—this is the efficient coding argument and it is the deep reason for centre-surround.
- Ambient illumination varies over 10 orders of magnitude between starlight and noon sun. Local contrast is roughly invariant though.

So retina encodes contrast, and the most important contrast is an **edge**, a place where intensity changes quickly. The derivative is the instrument to measure rate of change, so take the derivative of the image.

We take the second derivative to find maximums and minimums (where it is zero) in both $x$ and $y$ directions. That’s the **Laplacian**. 

**Gaussian smoothing.** A unit 2D Gaussian:
$$G_\sigma(x,y) = \frac{1}{2\pi\sigma^{2}} \exp\!\left(-\frac{x^{2}+y^{2}} {2\sigma^{2}}\right)$$
Convolving (applying as a filter) with it averages locally, weighted by distance, and removes fine detail.

**Difference of Gaussians.** Take two Gaussians of different width and subtract:
$$DoG(x,y) = G_{\sigma_1}(x,y) - G_{\sigma_2}(x,y), \qquad \sigma_2 > \sigma_1$$
This is the Mexican hat: positive centre, negative annulus, decaying to zero. It *is* the exact retinal circuit: a narrow excitatory pool from photoreceptors minus a broad inhibitory pool from horizontal cells.

What ration between $\sigma_{1}$ and $\sigma_{2}$?
- 1.75 is an empirical fit to measured retinal ganglion receptive fields
- 1.6 is the mathematical optimal that approximates Laplacian of Gaussian

Nature is close to the theoretical maximum!

**Laplacian of Gaussian.** 
$$\nabla^{2}G(r) = -\frac{1}{\pi\sigma^{4}}\left(1 - \frac{r^{2}} {2\sigma^{2}}\right)e^{-r^{2}/2\sigma^{2}}, \qquad r^{2}=x^{2}+y^{2}$$

