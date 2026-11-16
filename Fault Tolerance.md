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
date modified: Monday, November 16th 2026, 2:56:19 pm
---

Failure can be **transient**, **intermittent**, or **permanent**.

**Examples**: crash, omission, response, response, or Byzantine (adversarial, arbitrary).

### Addressing failure

Either through recovery algorithm or through redundancy.

- **Backward** recovery: return to previous correct state and continue
- **Forward** recovery: bring system to new correct state
	- Faster but harder

### Checkpoints

##### Independent

Each node independently records local state
- can be inconsistent
- 

##### Coordinated: Chandy-Lamport

