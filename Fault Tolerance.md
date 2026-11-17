---
tags:
  - distributed-systems
  - computer-science
type: note
author:
  - Gustavo Grancieiro
description:
aliases:
  - Distributed Systems Lecture 13
date created: Monday, November 16th 2026, 2:45:04 pm
date modified: Tuesday, November 17th 2026, 3:07:12 pm
---

We can address failure through either recovery algorithm or through redundancy.

- **Backward** recovery: return to previous correct state and continue
- **Forward** recovery: bring system to new correct state (faster but harder)

### Checkpoints

Independent checkpoint is when each node does arbitrary shit with their checkpoints with no coordination or global policy. It’s not consistent.

##### Chandy-Lamport

We define channel states $C_{xy}$ as messages sent but not yet received between $x$ and $y$.

**Requirements:**

- Global state changes **only** when something happens (not naturally or randomly)
- Channels are FIFO

1. Processes record locally their own state
2. Process work together with 

