---
tags:
type:
author:
description:
aliases:
date created: Monday, September 28th 2026, 12:29:11 pm
date modified: Monday, September 28th 2026, 12:29:18 pm
---
# Reconstruction

Gabor filters model the V1 cells receptive fields

Frequency domain vs space domain
Gaussian function
Laplacian function

Any gaussian convolve with delta function is gaussian itself centered at the specific frequency

Radio = frequency times signal

Gabor filter: gaussian in frequency domain
$$
\Phi(u,v)=e^{-\frac{1}{2}\left[ (u-u_{0})^2 \sigma^2 + (v-v_{0})^2 \beta^2 \right]}
$$
This is a gaussian shifted to $u_{0}, v_{0}$ is all we need to know

Convolution in the space domain becomes multiplication in the frequency domain

Modulation:
x is signal
$c(t)=\cos(w_{c}t+ \theta_{c})$

Fourier transform of a gaussian
The smaller the window in the frequency domain the bigger the window is in the space domain (because stdev becomes one over stdev, need to accept not understand)






