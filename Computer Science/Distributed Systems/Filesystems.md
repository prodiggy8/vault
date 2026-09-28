---
tags:
  - computer-science
  - course/15-440
  - distributed-systems
type: note
author:
description:
aliases:
date created: Saturday, September 26th 2026, 6:17:40 pm
date modified: Saturday, September 26th 2026, 6:17:47 pm
---
# Lecture 1

Goals:
- Caching
- Consistency
- Naming
- Security

We consider two examples developed concurrently: AFS and NFS.

AFS: make files appear local to authorized users on any computer
NFS: simple and fast server crash recovery (makes server stateless)

Distributed file systems provide transparent access to remote files.

Four design goals:
- Performance: much slower on network
- Consistency: coherent views when multiple people do shared data
- Naming: global schemes to locate files across administrative domains
- Security

Performance -> affects consistency
Naming -> affects security
Security -> affects performance

### The simple approach to DFS

Forward every operation via RPC
Server maintains copies

Simple, same behavior as if doing local filesystem
Can result in **terrible** performance
Server will get hammered

> Lesson: needing to hit the server for every detail impairs performance

##### How to solve this?

We want client-side caching!
Server-side caching doesn’t help with reducing the number of RPCs and network latency

The bad side of caching: **consistency**
If multiple clients cache the same file how do we keep their copies synchronized?
##### Block level (NFS)
Cache 4KB chunks independently
Efficient for large files, partial acess
Mixed versions within same file
##### Whole-file (AFS)
Simple consistency model
Wasteful for minor changes

Example:
- Server has “Hello”, A and B fetch
- B changes to “Hello world”, Server now holds that
- A still holds “Hello”

1. When to update: When should A see the updated version? Never automatically? On next file open? Immediately or within seconds?
2. Validation: How does A finds out his cache is stale? Server notification, periodic checks, assume valid until proven otherwise?

Strong consistency requires overhead
**You cannot maximize both performance and consistency**

Choose the **minimum** model application can support

## Strategy 1: Broadcast Invalidations

Server broadcasts “file invalid” who might have cached the file
Simple and efficient

Flaws:
- Network traffic explosion: N messages PER UPDATE for N clients
- Wasted messages: not everybody cached

## Strategy 2: Check-on-use

Before using cached data, client contacts server to verify cache entry is still valid
Strict, simple, and no server state

Flaws:
- Every read triggers network round-trip
- Server bombarded with validation requests
- Eliminates most benefits of caching

## Strategy 2B: NFS v2

Attribute caching with timeouts!

Good: reduction in server load
Lost: strict consistency

## Strategy 3: Callbacks (AFS)

When client caches a file, server records in a **callback list**
Server promises to notify if file changes. Client trusts cache until callback is received.

- Server now needs a state! List of clients’ caches
- Clients must track callbacks

Complexity cost: server crash -> lost state, requires revalidation of **all** cached files
FAST

## Strategy 4: Leases

**Time bounded consistency guarantee:** lease grants client right to cache data for some time. Promises **not to allow** modifications until then.

Multiple clients can hold **read leases**.
Only one can hold **write** ones. Can write locally but must **send writes** before lease expires.

Pros: bounded inconsistency, automatic cleanup, predictable state, failure resilience 
(stateless)

Cons: loose clock synchronization, lease renewal protocol (complex)

WIDELY USED IN DISTRIBUTED SYSTEMS

# Lecture 2

# Consistency

Unix local filesystem
- Read returns **latest** write
- Writes are immediately visible to all processes
- File operations are atomic and serialized

NFS: **close-to-open** + attribute caching

- writes visible to other clients on close