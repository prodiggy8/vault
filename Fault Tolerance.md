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

- Global state changes only upon event
- Channels are FIFO
- Channels are reliable

To **initiate** a snapshot:
1. Process logs its own local state
2. Broadcasts a **marker message** before anything else
3. Process records every message arriving on each of its incoming channels

When process $P$ **receives** a marker on channel $C$:

- If it’s the first marker it has seen
	1. Log its own local state
	2. Log channel $C$’s state as empty
	3. Sends marker on all outgoing channels
	4. Starts recording messages arriving on all its **other** incoming channels

- If $P$ has already recorded its state
	1. $P$ stops recording on channel $C$. The state of $C$ is every message that arrived on $C$ between $P$