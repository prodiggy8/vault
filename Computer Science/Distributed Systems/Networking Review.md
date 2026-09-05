---
tags:
type:
author:
description:
aliases:
date created: Thursday, August 27th 2026, 12:03:12 pm
date modified: Thursday, August 27th 2026, 12:03:15 pm
---
## Lecture 1

Cables for everyone: $n^2$ wires!
Alternative: switching

**Circuit Switching**
- Dedicated connection (circuit)
- Torn down after usage
- Telephone system
- Fast, stable, predictable

**Packet Switching** 
- Packets travel independently
- Switches decide how to forward each
- General for many different needs (bursty traffic averages out)
- Efficient, robust, better resource sharing

**OSI Model**
- All devices implement physical
- After that only necessary layers are implemented
	- Switches have until data link
	- Routers until network
	- Hosts have complete stack
- Travel from higher to lower layers using encapsulation
- **Layers can have multiple protocol implementations**
	- UDP vs. TCP
	- Ethernet vs. Wireless
	- Demultiplexing field in headers
### Where to place functionality?

“End-to-end argument in system design.” Saltzer, Reed, and Clark.

A function should be implemented at the endpoints of a communication system. Only endpoints know what “correct” means for their application, so any lower layer trying to guarantee correctness will be incomplete.

**Example:** File transfer. Network could add checksum and retransmission at every hop, but it doesn’t protect against a bad disk read at one end or a memory corruption in the other end. The ends need to do the verification anyway.

Checksum done in data link or network are merely performance optimizations, it doesn’t guarantee correctness.

## Lecture 2

Flat vs. hierarchical addressing

MAC addresses are flat
IP addresses are hierarchical

Switches use forwarding tables to forward data (MAC)
- Flat addressing implies tables need to store all possible addresses

IP uses hierarchical addressing
Prefix + suffix based on class
Assignment is dynamic and local (can be done with DHCP)
Even class structure was not enough

Switch to classless model (IPv6)
NAT -> hosts share IP addresses
- CIDR: flexible division (/prefix)
- 

