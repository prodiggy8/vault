---
tags:
  - computer-science
  - computational-perception
  - perception
type: note
author:
description:
aliases:
date created: Sunday, October 4th 2026, 2:28:16 pm
date modified: Sunday, October 4th 2026, 2:28:19 pm
---
**Spatial frequency:** high means fine detail and sharp boundaries, low means large-scale layout.

For instance, the Mona Lisa seem to smile at low frequency. We we focus and see higher detail it disappears.

### Decomposing image into frequency bands

Continuously blur: $g_{0} = I, g_{1} = G * g_{0}, g_{2} = G * g_{1}, \dots$ with each Gaussian keeping structure coarser than some scale.
We take differences:
$$L_{k} = g_{k} - g_{k+1}$$
This is the band of detail lost between blur levels $k$ and $k+1$.

**A blurry image doesn’t need all its pixels:** dropping every other sample loses almost nothing.

## The Gaussian pyramid

$$g_{l}(i,j)=\sum_{m=-2}^2 \sum_{n=-2}^2 w(m,n)g_{l-1}(2i + m, 2j + n)$$
Each level has half the width and height or the one below. Total storage is $\frac{4}{3}$ of the original.

The kernel needs to be:
- Separable (so the 2D filter can be applied in two 1D passes)
- Normalized (so average brightness is preserved)
- Symmetric $w(i) = w(-i)$
- Equal contribution for each node at level $l-1$ to weight of level $l$

## Laplacian pyramid

Predict a finer level from a coarser one by inserting zeroes between samples and interpolating with the same kernel.
$$g_{l,1}(i,j)=4 \sum_{m=-2}^2 \sum_{n=-2}^2 w(m,n)g_{l}\left( \frac{i-m}{2}, \frac{j - n}{2} \right)$$
