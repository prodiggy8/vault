---
tags:
type:
author:
description:
aliases:
date created: Sunday, October 4th 2026, 6:55:23 pm
date modified: Sunday, October 4th 2026, 6:55:26 pm
---
Analysis:
$$F(k)=\sum_{n=0}^{N-1}f(n)e^{-i 2 \pi kn / N}$$
Read as: each coefficient is the projection (dot product) of the signal on one basis wave.

Synthesis:
$$f(n)=\frac{1}{N}\sum_{k=0}^{N-1}F(k)e^{i 2 \pi kn / N}$$
Read as: the signal is a weighted sum of $N$ basis waves, and the weights are the weights are the Fourier coefficients.

##### For a 2D N x M image

$$F(u,v)=\sum_{x=0}^{N-1} \sum_{y=0}^{M-1}I(x, y)e^{-i 2 \pi (ux/N + vy/M)}$$
