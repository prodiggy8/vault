---
tags:
  - distributed-systems
  - computer-science
  - course/15-440
type: note
author:
description:
aliases:
date created: Saturday, September 26th 2026, 6:09:01 pm
date modified: Saturday, September 26th 2026, 6:09:05 pm
---
**Remote Procedure Calls** are abstracted procedures. Instead of formatting and sending messages to server we just appear to be calling a local method. RPC subsystem will handle format, messaging, timeouts, retries, etc.

**Transparency:** hiding the distributed nature of the system.

High transparency means the system appears to be a single server, remote calls appear to be local, more abstractions. Examples: Google Photos, iCloud, etc. Low transparency examples would be P1 and EC2.

Several dimensions of transparency (location, access, concurrency, replication, failure, etc). We focus on access.

RPCs sit between distributed applications and local network/OS services, i.e., in the form of a library.

### RPC package in Go

```go title=RPC
type Arith int
type Args struct { A, B int}
func (t *Arith) Multiply(args *Args, reply *int) error {
	*reply = Args.A * Args.B
	return nil
}
```
```go title=Server
arith := new(Arith)
rpc.Register(arith)
rpc.HandleHTTL()
l, e := net.Listen("tcp", ":1234")
go http.Serve(l, nil)
```
```go title=Client
c, e := rpc.DialHTTP("tcp", serverAddress + ":1234")
args := &server.Args{7,8}
var reply int
err = client.Call("Arith.Multiply", args, &reply)
```

### Stubs

Code that handles de/serializing RPC arguments

**Client:** *marshals* (i.e. serializes, pickles) arguments into machine-independent format, sends requests to server, waits for response, *unmarshals* response

#### Writing an RPC by hand

```c title=Stub
struct Arith_msg {
	uint8_t operation;
	uint32_t A;
	uint32_t B;
	
void Arith_multiply_stub(int A, int B, int* reply) {
	int msglen = sizeof(struct Arith_msg)
	char buf = malloc(msglen)
	struct Arith_msg *am = (struct Arith_msg *)buf;
	am->A = htonl(A)
	am->B = htonl(B)
	write(outsock, buf, msglen)
	free(buf)
	// same for the read!
}
```



`htonl` is host to network-byte-order, long.
We basically convert to big endian because the network operates on it.

Three things that make transparency difficult:
- Memory access -> **we don’t do that**
- Failures
	- In distributed systems **machine failure is indistinguishable from network failure**
	1. We can make identical to local: partial failure triggers complete failure, system crashes.
	2. Break transparency: 
		- If it’s
		- sometimes it’s okay to repeat the call (if idempotent).
- Latency

