---
tags:
  - system-design
  - book/system-design
  - computer-science
type: chapter
author:
  - Alex Xu
description:
aliases:
date created: Sunday, October 25th 2026, 1:40:05 pm
date modified: Sunday, October 25th 2026, 1:40:20 pm
---
##### Database

With a growing user base, one server is not enough. Usually the next step is a database server.

**When to use non-relational?**
- Application requires **super-low** latency
- Data is unstructured
- Only need to serialize and deserialize data
- Need to store a **massive** amount of data

**Replication**
- Usually with a master/slave relationship between the original and the copies
- Master can write, replicas can read
- Most applications require many more reads than writes
- 
##### Load Balancer
Evenly distributes incoming traffic among web servers. Usually load balancers communicate with web servers through private IPs and they are unreachable to the internet.

