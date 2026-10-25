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
##### Load Balancer
Evenly distributes incoming traffic among web servers. Usually load balancers communicate with web servers through private IPs and they are unreachable to the internet.

##### Cache
*Read-through cache:* make the cache a gateway. Every request polls cache first. If unsucessful cache saves result after querying from the database. 

- Consider cache when data is read frequently and written infrequently
- Expiration policy
- Consistency (for details read “Scaling Memcache at Facebook”)
- Single point of failure: multiple cache servers are recommended.
- Eviction policy: LRU, LFU, FIFO.

**Content Delivery Network**
It’s just a cache of static content (CSS, JS, images, videos, etc) replicated across the world to mainly counter geographical latency.
- Usually third party
- Also has to think about expiry
- Clients should detect when CDN is down and request from origin

### Horizontal Scaling of the Web Server
- State needs to be out of the server, like in the database.
- For stateful servers you need to route each client to the same server. Called **sticky session** and is implemented in most load balancers.

#### Message queue
- Pub/sub
- A bugger and distributes asynchronous requests
- Then messages are published even when the consumer is unavailable to process

#### DevOps
- Logging and monitoring: per server or aggregated to centralized service (like DataDog)
- Metrics: like CPU, Memory, disk I/O, aggregated level metrics, key business metrics.
- Automation

### Database Scaling
- Vertical: with RDS, for instance, you could get 24 TB of RAM.
- Horizontal: also known as **sharding**
	- Data is **unique** to the shard, however they share the same schema
	- Hash function finds the shard
	- **Sharding key:** determines how data is distributed

