---
tags:
type:
author:
description:
aliases:
date created: Tuesday, October 20th 2026, 9:30:58 pm
date modified: Tuesday, October 20th 2026, 9:31:02 pm
---
# LSP

Live Sequence Protocol, between TCP and UDP.

- Client-server communication model
- Message sizes are limited to fit within single UDP packets (1,000 bytes)
- Messages sent reliably – exactly once delivery and same order
- Message integrity ensured – rejected if modified in transit
- Server and clients detect when other side has disconnected

#### Message format

**Message type:**
1. Connect
2. Data
3. Ack
4. CAck – a cumulative ack for multiple messages

**Connection ID:** positive integer
**Sequence number:** for ordering, starts with a client-chosen 32-bit nonce for the initial connection request (no worries with overflow)
**Payload Size**
**Checksum:** 16-bit number derived from the message
**Payload**

Connect, Ack, and CAck have payload values of nil.

- Connect must have connection ID **zero**, server Acks with real ID
- Ack carries ID and sequence number
- CAck carries the same, it Acks all of the previous messages up to sequence number

##### For now, no messages are dropped

- Server and client will maintain **their own separate series of sequence numbers**
- My implementation needs not to use CAcks but must be able to recognize it

**It’s possible to receive messages while waiting for Acks**

Sliding window protocol: $\omega$ is number of messages that can be sent without acknowledgment
- If $n + \omega - 1$ were sent then a new one can only be sent when **the oldest message $n$** is acked.

On top of that the server has a limit $M$ of unacked messages. So the limit is really $\min(\omega, M)$

### Epoch Events

