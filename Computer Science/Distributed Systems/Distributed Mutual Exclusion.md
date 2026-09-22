---
tags:
  - computer-science
  - course/15-440
  - distributed-systems
type: note
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Monday, September 21st 2026, 5:22:46 pm
date modified: Tuesday, September 22nd 2026, 12:07:33 am
---

Scale up (vertical): add resources to single node

Scale out (horizontal): add more nodes to distributed system.

- Application has to conform
- How to coordinate access to shared resources?

> [!warning] Recall desired properties of concurrency
> Just one process at one time at the critical section
> Requests to enter the critical section eventually succeed
> Access/delay to critical section is approximately equitable
> Don’t waste resources

## Centralized mutual exclusion

- Process 1 requests mutex (granted)
- Process 2 requests mutex (queued)
- Process 1 releases mutex (granted to process 2)

- Clearly safe
- 3 messages per mutex access (expensive)
- Central coordinator is single point of failure

#### Bully leader election

1. Process P notices leader has failed
2. Sends election message to all process with higher numbers
3. If no one responds, P wins the election and becomes coordinator
4. If one of the higher-ups responds, it takes over. P’s job is done.

Example:
- 7 is down. 4 notices and calls an election
- 5 and 6 responds, 4 is done.
- 5 and 6 both hold an election.
- 6 responds. It wins and tells everyone.

## Decentralized mutual exclusion

With $n$ coordinators.
To get mutex: get a majority vote from $m>\frac{n}{2}$ coordinators.
All respond with grant or deny.

If fewer than $\frac{m}{2}$ votes: backoff and try again.

- Majority ensures safety
- Fairness depends on random chance
- $2km+m$ messages for $k$ attempts to get a majority.
- Risk of starvation.

## Totally-ordered multicast

1. Message to be sent is timestamped with sender’s logical time (Lamport)
2. Multicast (sender included)
3. When message is received
	- Put in local priority queue ordered according to timestamp
	- Receiver multicasts acknowledgement

Message delivered to applications only when:
- Head of queue
- Acknowledge by all involved processes


more to do here…

## Ricart and Agrawala mutual exclusion

Relies on Lamport once again

- When a node wants to enter critical section, sends timestamped requests to all other nodes; they eventually reply.
- Can enter when received replies from all others
- **A node with earlier request doesn’t reply until after it has exited the critical section**

Receiving end:
- Doesn’t want resource: responds yes
- Using the resource: queues the request
- Wants to use the resource as well: compares timestamp—lowest wins!

**Proof of correctness**

Suppose $A$ and $B$ are allowed to be in critical section at the same time.
- $A$ must have sent a request and gotten a reply; same for $B$.
Case 1: one received the request before the other sent the request
- If $B$ received request from $A$ before requesting, then $T_a < T_b$ and $A$ would not replied before leaving the critical section.
Case 2: both sent requests before receiving from the other
- Still, $T_a$ and $T_b$ must be ordered. Suppose $T_{a} < T_{b}$, $A$ would have not sent a response.

- Since ordered, cannot have a deadlock! It **must** be that the time of one request is lower than the other.

- If node made request it would be granted eventually.