---
tags:
  - computer-science
  - computational-perception
  - perception
type: note
author:
description:
aliases:
date created: Sunday, October 4th 2026, 1:45:04 pm
date modified: Sunday, October 4th 2026, 1:45:10 pm
---
**Why the inverted retina?** 
Probably because photoreceptors need to regenerate their pigment through the *epithelium* behind them. If it was normally arranged it couldn’t be in direct contact.

**Why foveated vision?**
Covering the whole field at foveal resolution would require a gigantic optic nerve. We wouldn’t be able to rotate our eyes. Sample the periphery coarsely and point the fovea at it when something interesting happens.

The disadvantage is we need attention to sample details (Chapter 1).

## Computational model

A transformation from input to output, according to a rule. In the LoG model the input is the image, the rule is LoG, and the output is the contrast. Vision is a series of such computations.

#### Marr’s three levels of explanation
- What is computed and why?
- How (algorithm)?
- How the physical organism implements it?

## Hermann Grid

The classical explanation says it’s because of center-surround (4 black corners).
It even predicts that when we focus it disappears because foveal field is small.

This breaks!
- If streets are wavy, the illusion disappears although centre-surround layout is still there
- With grey and white streets the illusion is enhanced ONLY when the grey is in the front.

So the model is missing something: **orientation and surface/depth interpretation**. The illusion is probably cortical, not retinal.

