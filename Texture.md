---
tags:
type:
author:
description:
aliases:
date created: Monday, October 5th 2026, 11:02:10 am
date modified: Monday, October 5th 2026, 11:02:12 am
---
Texture is judged by statistics

Julesz
- Textures with same pixel pair statistics look the same
- Counterexamples proved it wrong
- Better: count **textons**, local features like line ends, corners, crossings, orientaitons.
- Orientation differences pop out, flipping light/dark doesn’t. Groupings uses complex cells

Testing by synthesis:

- Portilla Simoncelli: match how filter outputs relate across positions, orientations, scales. (Use correation and phase, not texton counts)
