---
tags:
type:
author:
description:
aliases:
date created: Monday, October 5th 2026, 10:21:08 am
date modified: Monday, October 5th 2026, 10:21:25 am
---
Hubel and Wiesel: orientation selectivity

V1 simple cell sums outputs of several LGN centre-surround cells whose filed lies along a line.

Neighboring points in visual field -> neighboring in V1
Orientation columns (rotate across cortical surface)
Ocular dominance columns
Hypercolumn: full set of orientations for both eyes
___

Modeled by Gabor function: Gaussian envelope times a sinusoidal carrier.
$$
G_{\sigma_{1}, \sigma_{2}} \cos(kx + \phi)
$$
Where:
$k$ is spatial frequency of the stripes
$\sigma_{1}$ width of the envelope across stripes
$\frac{\sigma_{2}}{\sigma_{1}}$ elongation along the preferred orientation
$\phi$ even symmetric, bar detector, odd anti symmetric, an edge detector.

Band-pass like DoG but only for one orientation, DoG is for all.

Uncertainty principle: filter that is very precise about where a feature is cant be precise about which frequency. Gabor achieve the minimum.

# Reconstruction

Modulation: smooth signal * wave moves frequencies to the wave’s. Gabor is Gaussian * wave so it is a gaussian filter moved to some frequency.

Cells in v1 are few, their RF overlap. Inhibit neighbors that overlap with own RF. Until together they rebuild image perfectly. Takes time: looks like filling in.

Filling in: in blind spot yes, Troxler fading no.
	Fixate steadily fuzzy disk in periphery fades and is replaced by surround color.
	Neurons in V1 follow physical stimulus, not perceived filled-in color.

## Isomorphic
Neural activity spread across 2D cortical map like paint. Early cortex holds a picture of the perceived surface.

Blind spot experiment.

### Symbolic
Early areas only detect boundaries. Higher areas interpret or label, without changing early cortical activity

Troxler fading is in favor

## Complex CElls
- Orientation tuned but respond to a bar anywhere in the RF and to both light and dark bars.
- Do not care about position (phase)

