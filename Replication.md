---
tags:
  - distributed-systems
  - computer-science
type: note
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Thursday, November 19th 2026, 9:14:56 pm
date modified: Thursday, November 19th 2026, 9:48:55 pm
---

# Consistency

**Strict**

Any read operation returns the value of the most recent write operation on that item, as if all operations occur instantaneously.

**Sequential** 

All reads and writes can be placed in *some* global order in a way that they’re consistent with local orders at each replica.

- Sometimes there is no global order that works.

**Causal**

All nodes see causally related writes in the same order. But concurrent writes may be seen in different order at different replicas.

![[Replication.png]]

This is not causally consistent because there’s a causal relation between reading $a$ and writing $b$, we can’t read $b$ first because we know $a$ happened before.

# State machine replication

Replicas should stay in **sync** with each other

- start in same state, apply the same state transitions

Can be achieved by replicating an append-only log

- we need replicas to agree on global order for the logs

#### Simplification

We can run a consensus algorithm once per log entry, to consistently determine the next entry in the log.

- Run repeatedly

**Fischer-Lynch-Paterson** **result**

> No deterministic 1-crash-robust consensus algorithm exists with asynchronous communication

**Strong assumptions**

- Deterministic algorithm
- Asynchronous communication means no shared clock, unbounded message delay
- We need to “fully” achieve consensus — in many systems we can get consensus the vast majority of times

# Paxos

- Allow proposals for any server, any time
- Some algorithm choose the single consensus one

**Safety**
- Only 1 chosen
- Must have been proposed by someone
**Liveness**
- Some value eventually chosen
- Servers eventually learns it
- **Liveness can be sacrificed in the name of safety**
**Fault-tolerance**
- if $<f$ nodes fail, the rest should reach consensus with high probability

#### Roles
- **Proposers**
- **Acceptors** (vote on proposed values, store accepted, reach consensus)
- **Learners**

Each participant can have more than one role. Usually they all have the three.

**Quorum** is a subset of participants such that any two are guaranteed to intersect.
- a “majority”
- in Paxos, it’s the any majority of acceptors

#### Failure model

Works on:
- Asynchronous network: arbitrary delay, duplication, reordering, network partitions can happen
- Server failures: process may crash at any time, are not required to recover (given $<f$)
- Persistent state: we need to be able to read and write persistent storage, including when node reboots from crash
- Non-byzantine faults: crashes cannot be intentionally malicious

## Paxos: multiple rounds of two phases

1. **Prepare**

Proposer sends proposal number to acceptors
- numbers are globally ordered, distinct
- anyone can send at any time

Acceptors:
- promise not to accept a lower-numbered proposal
- or they can reject

If promises not received from majority of acceptors, restart Phase 1 with a higher proposal number

2. **Accept**

Proposer asks acceptors to accept their proposal number and value

Acceptors accept or reject

If proposal not accepted by majority, restart Phase 1 with higher proposal number

___
Example:
- Prepare(n)
- Promise(n, ni, vi) where ni, vi are value already accepted previously
	- or NACK(Ni) where Ni is highest seen so far
- 