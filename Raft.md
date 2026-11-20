---
tags:
type:
author:
description:
aliases:
date created: Thursday, November 19th 2026, 11:49:03 pm
date modified: Thursday, November 19th 2026, 11:49:05 pm
---
Raft sequences client requests into a log and ensures replicas agree on the contents and ordering of the log.

- Each replica asynchronously applies client requests in order they appear in the log.
- If replica fails, Raft brings the log up to date.
- Will continue as long as majority is alive
- If majority dies, then waits for it to come back alive

Log entry: command and index number
After log is committed, Raft “applies” log by sending committed log entry to application

**Paper only if time allows**

1. Follower
2. Candidate
3. Leader

All nodes start follower
If followers don’t hear from a leader, they can become candidates
- Request votes as such
- Candidate becomes leader if majority vote

All changes now go through the leader. But the leader must commit changes.
To commit:

1. Replicates log to follower nodes
2. Wait until majority has written the entry
3. Commit
4. Notifies followers entry has been commited

#### Election

Election timeout: amount of time a follower waits until becoming a candidate
- Randomized between 150ms and 300ms

If receiving node hasn’t voted, votes for the first request that arrives, and reset election timeout.

Leader begins sending append entries to its followers.
- These messages have a heartbeat timeout
- Followers respond

Continues until heartbeat stops and node becomes candidate again.

###### Split Vote

- Will tie and not achieve majority.
- Just wait and try again
- Since interval random someone will get headstart

#### Log Replication

- Same append message as in heartbeats

___
Suppose network partition:
- Two leaders will appear, election in one of the partitions
- At least one won’t have a majority so they can’t commit!

Once network is back, old leader will see higher election term and step down.
Members of one partition will catch up to match new leader’s log
___

### Safety

Core guarantee: once entry is committed, every future leader has it, so no server ever applies a different command at that index.

**Election restriction**
- Server refuses its vote unless the candidate’s log is at least up to date with its own:
	- Candidate’s last entry has higher term
	- Last terms are equal and log is at least as long

Committed entry is on majority, winner needs majority. The two overlap in at least one server and that server would refuse the vote based on this rule.
- So a server cannot win without a committed entry.

**Count replicas only for the current term**

- 