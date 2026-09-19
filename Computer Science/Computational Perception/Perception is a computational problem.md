---
tags:
  - perception
  - computer-science
type: note
author:
description:
aliases:
date created: Saturday, September 19th 2026, 2:36:51 pm
date modified: Saturday, September 19th 2026, 2:37:08 pm
---
Vision is hard.

Image formation throws information away, and perception has to put it back.

A 3D scene with a given illumination, surface reflectance, and geometry projects to a 2D array of intensities. That projection is many-to-one. Infinitely many scenes produce the same image — a white surface in shadow and a gray surface in light produce the same pixel values.

Going forward (scene -> image) is physics and is well-posed. Going backward (image -> scene) is what the visual scene does and it is **ill-posed**: the data alone doesn’t determine the answer.

The brain draws from previous experiences, assumptions about light and surface, statistics of natural scenes, etc, to fill this gap.

From Marr’s: **"vision is an inverse problem.”**

#### Demos

1. One person describes the Repin “An Unexpected Visitor” painting and other pictures it.

**Takeaway:** a visual representation supports an enormous number of possible downstream queries; a linguistic description has already committed to a small subset of them. People decide what matters and what not in the picture.

People also differ in narration structure. Some go left-to-right (serial), others give scene gist first and then details (hierarchical). Hierarchical ones transmit better.

2. Same task but viewer gets 2 seconds.

Mary Potter’s experiment gave viewers 100ms and they still were able to do it.

**Takeaway**: parallel intake versus serial report. Viewers extract a lot at once from picture. The description that follows takes much longer, words come out one at a time.

#### Active perception

Some students asked questions. You do not passively receive a scene. You have a model, identify what’s uncertain, and move your eyes to gather evidence that resolves it.

**Yarbus:** recordings of eye movements on the exact painting from image 1 show scan paths changes depending on the question the observer has been asked.