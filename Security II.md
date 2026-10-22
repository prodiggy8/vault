---
tags:
  - distributed-systems
  - security
  - computer-science
type: note
author:
description:
aliases:
date created: Thursday, October 22nd 2026, 11:03:27 am
date modified: Thursday, October 22nd 2026, 11:50:01 am
---

### Symmetric Key Distribution

Key Distribution Center: shares pairwise secret keys with *each* registered user

1. Alice sends $K_{A-KDC}(A,B)$ to KDC
2. KDC generates ticket R1 (session key)
3. KDC sends $K_{A-KDC}(R1, K_{B-KDC}(A, R1))$ to Alice
4. Alice decrypts message & sends inner argument to Bob
5. Alice and Bob now communicate with R1

Now we only need $n$ keys.

- KDC must be online at all times or nobody talks
- Centralized trust and point of failure

### Public Key Infrastructure

System that is trusted and binds public keys to entities

Certification authorities:

1. Entity proves its identity to CA
2. CA provides certificate binding Entity to its public key
3. Certificate contains public key and CA’s signature (using its key)
4. Can be verified with CA’s public key

- TLS/SSL
- The CA doesn’t have to be constantly contacted as long as you have its public key (also an expiration date)
- Can’t revoke fast!
	- Only on timeout
	- There is an on-line revocation authority that distributes a revocation list, it works since it’s rare.

### Diffie-Hellman

- See 15251 notes [[Cryptography]]

## Access Control (Authorization)

Access Control Matrix — **who** can do **what** to **what/whom**
- e.g. user x files x r|w|x

Doesn’t scale, sparse matrix

- Order by columns (Access Control List)
	- e.g. Andy: { (file_1, rw), … }
	- This is Linux’s model
	- More common in the past

- Order by rows (capability lists)
	- e.g. file_1: { (Andy, Bob, …) }
	- Systems today are more suited for this system (e.g. IAM in Cloud)

## Randomized Routing

- Hide message source by routing it randomly
	- Crowds (technique), Freenet (network), Onion (network)
- Routers don’t know if source is really the sender or another router




