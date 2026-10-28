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
# Concepts
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


# Estimates

**Mean times:**
- L1 cache reference -> 0.5 ns
- L2 cache reference -> 7 ns
- Mutex lock/unlock -> 100 ns
- Memory reference -> 100 ns
- Compress 1 KB -> 10 $\mu$s
- Send 2 KB over 2 Gbps network -> 20 $\mu$s
- Read 1 MB from memory -> 250 $\mu$s
- Round trip same datacenter -> 500 $\mu$s
- Disk read -> 10 ms
- Read 1 MB from network -> 30 ms
- Read 1 MB from disk -> 30 ms
- Send packet CA to Netherlands round trip -> 150 ms

1. Cache -> memory -> disk
2. Compress before sending anything, it’s fast
3. Network is horribly slow, don’t send data between data centers

**Availability:**

99% -> 14 minutes down per day
99.9% -> 1 minute
99.99% -> 8 seconds
So on.

**Practice:**
- QPS
- Peak QPS
- Storage
- Cache
- Number of servers

# Framework

1. **Understand the problem and establish design scope**

- Not a trivia contest, don’t give out answers too quickly
- Ask questions to clarify requirements
- Functional and non-functional requirements
	- How many users?
	- How fast to scale up? Anticipated scale in 3 months and 1 year
	- Current tech stack of the company?
	- Existing services that can simplify the design

2. **Propose high level design and get buy-in**

- Box diagram with key components
- Ask for feedback, treat interviewer as a teammate
- Database schema and API endpoints **only if the problem is tiny**

1. **Deep dive**
___
**Rate limiting**

# Rate Limiting
- Token bucket
	- Places tokens, requests consumes
	- Supports bursty traffic
- Token queue
	- Requests placed in limited-size queue and processed at a fixed rate
	- Does not support bursty traffic
- Fixed window
	- Almost like token bucket, time window number of requests per window
	- Allows bursty traffic (send before reset, can double rate effectively)
- Sliding window
	- Consumes lots of memory to keep track of requests’ timestamps
- Sliding window counter (mix between previous 2)
	- $\text{\# requests curr } + \text{\# requests prev } * \text{ overlap \% of rolling and prev window}$
	- Smooths out spikes, memory efficient

Store counters in cache (supports time based expiration)

- Return to client in API headers that tell how many requests are left.
- Just describe in API docs and let client figure it out

In distributed environment:
- Race conditions on counter can happen
- Just use transactions
- Sticky sessions also work

##### Consistent Hashing

Definition: if table is resized, only $\frac{n}{m}$ keys need to be remapped.

# KV-store

API types
- Rest: HTTP methods to manipulate resources IDed by URL. Default
- GraphQL: single endpoint with query language — when variation like dashboard vs. mobile app to avoid many requests
- RPC: marshalling, distributed systems

