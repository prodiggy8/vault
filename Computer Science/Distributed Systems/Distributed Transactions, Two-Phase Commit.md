---
tags:
  - computer-science
  - distributed-systems
  - transactions
  - course/15-440
type: note
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Wednesday, September 30th 2026, 11:43:40 am
date modified: Wednesday, September 30th 2026, 11:43:49 am
---
- How to atomically and concurrently access multiple-objects, across multiple-servers

## Transactions

In **composite operations** there are two challenges:
- Insufficient atomicity: we want all or nothing
- Fault tolerance

A **transaction** is a set of operations that happen as if they were a single, indivisible operation.

### ACID Properties

1. **Atomicity:** Either completes entirely or is aborted; if aborted, no effect on shared state.

2. **Consistency:** Preserves set of invariantes about shared state.

3. **Isolation:** Executes as if it were the only one with ability to read or write shared state.

4. **Durability:** Once transaction has been committed, its effects persist even in the presence of failures.

> [!Definition] Serializability
> A schedule of transaction operations is **serializable** if it is equivalent to some serial ordering of the transactions.

**Example:**
- `transfer(x, y, 60)` and `transfer(x, z, 70)` with `balance[x] = 100`
- If one goes first then the other, the last fails.
- If they’re concurrent:
	- Both read the balance and see `x` has enough
	- Both update the balance to a different number (either `30` or `40` whichever comes last) and both transfers succeed
	- This is wrong.

###### Locks
- Single lock works but whole thing becomes sequential bottleneck
- Fine grained locks deadlock (`op(x, y) and (y, x)` as in homework)
- Solution is **global ordered locks**
```
transfer(i, j, v):
	lock(min(i, j)); lock(max(i, j))
	if withdraw(i, v):
		deposity(j, v):
		
	unlock(i); unlock(j);
```

### The waits-for graph

Vertices represent transactions
Directed edge if transaction $i$ is waiting for lock held by transaction $j$
Deadlock **if and only if there is a cycle in the graph**

Locks in global order -> **can’t deadlock**

## Two-phase locking (2PL) for serializability

**Phase 1:** Acquire locks as txn progresses, no locks released
**Phase 2:** Release locks in phase 2, no locks acquired

Commit: apply changes, release locks
Abort: discard changes, release locks

Example:
```python
transfer(i, j, v):
	L = {i, j} // locks
	U = []     // updates
	if Bal[i] >= v:
		U.append(Bal[i] -= v)
		U.append(Bal[j] += v)
		commit(U, L)
	else:
		abort(L)
```

Deadlocks can still occur:
- Transaction may not know all the locks it needs ahead of time

Ways to handle:
- Lock manager builds the graph. On finding a cycle, choose offending transaction and force abort
- Use timeouts: transactions should be short. If hit time limit, find transaction and force abort.

# Distributed Transactions

We can have distributed databases. Example: `i` is in one server (responsible for `withdraw`) and `j` is in another (responsible for `deposit`)
**All servers** must agree to commit or abort. 

- Coordinator server
- Ensures all reach the same decision
### Phase 1A
- Coordinator sends prepare to participants
### Phase 1B
- Participants log vote to disk and respond with vote
### Phase 2A
- Coordinator checks votes and makes decision: commit if all vote commit
- Persist to disk before green lighting
### Phase 2B
- Write decision to disk, complete transaction, send ACK
- Coordinator persists END to disk
___
Must abort if any voted abort

# Failure and Recovery

- Recover from log on disk

Participant fails with no logged abort/commit
- Set timeouts to wait for participant
- Upon recovery participant doesn’t see a logged decision and aborts

Participant fails with logged vote abort
- Coordinator sees vote, aborts
- Participant unilaterally aborts after seeing local VoteAbort

Participant fails with logged vote commit
- Ask the coordinator for decision
- If within timeout, it will abort, otherwise send correct answer

Coordinator fails with logged COMMIT without an END
- Broadcast commit decision



Possibilities:
Before prepare or before write vote
- 1 minute down
- Once wakes up does nothing
- Coordinator sends request every ms so 1 extra ms once awake
Total: no failures + 1 minute

Before send vote
- 1 minute down
- Same thing as before

Before write receiving or writing commit
- 

Before ack (before or after completing operation)