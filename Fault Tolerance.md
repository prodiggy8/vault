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
date modified: Wednesday, November 18th 2026, 3:07:22 pm
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

Snapshot initiation by $P$

1. $P$ records own state
2. $P$ sends marker message to everyone
3. $P$ starts recording on its incoming channels

When $P$ receives marker message from $C$

- If it’s the first marker it has seen
	1. Record own state
	2. Mark $C$ as empty
	3. Propagate marker to all other outgoing channels
	4. Starts recording messages arriving on all its **other** incoming channels

- If $P$ has already recorded its state
	1. $P$ stops recording on channel $C$

Snapshot termination

1. All processes have received a marker on **all** incoming channels
##### Takeaways

