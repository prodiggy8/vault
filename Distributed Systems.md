## Question 1

You are an engineer at GDB (Goldman De Berkshire) tasked with designing a distributed banking system. GDB operates three bank branches, each running on its own server process:

- B1 = New York
- B2 = London
- B3 = Singapore

Each branch handles deposits and withdrawals locally as internal events, and occasionally sends fund transfers to another branch. Because transactions span multiple continents, the bank needs to take consistent snapshots to understand its global balance without stopping the system. To do so, GDB’s engineers have designed a Chandy-Lamport snapshot algorithm.

As your first intern task, GDB would like you to check some traces of their algorithm to ensure it is correct. You have been given a trace where the starting balance of each branch is as follows:

- B1 $100 billion
- B2 $45 billion
- B3 $68 billion

In the trace, dots represent both internal and external communication events. If a dot has no incoming or outgoing arrows, it is an internal event. A dot with an outgoing arrow is a send transfer event. A dot with an incoming arrow is a receive transfer event. The branch state at a given time is the set of all events that have occurred before that time. For example, the state of B1 by the end of the execution trace below is {A, B, G, J, N, Q}. For any channel state that is recorded, we note down both ends of the events. For example, a possible channel state where B2 initiates a transfer at event C and B3 receives that transfer at event E is: B2->B3: [C->E]. The execution trace also uses dotted arrows (- - - >) to represent marker messages.

![[Distributed Systems.png]]

1.1 Which branch initiates the snapshot?

1.2 What is the snapshotted state? 
B1: [ ], B2->B1: [ ], B3->B1: [ ]
B2: [ ], B1->B2: [ ], B3->B2: [ ]
B3: [ ], B1->B3: [ ], B2->B3: [ ]

1.3
What is the balance for each branch in the snapshotted state?  
_Note 1: internal events do not affect the balance of a branch Note 2: transfers captured in-transit are not considered executed. For example, if B1 and B2 have the following state: B1: [A], B2: [], B1->B2: [A->C]. The transfer is not considered executed. B1 and B2’s balances do not change._

1.4 Suppose that want to describe a snapshot that would result in the following balances being snapshotted: B1: $99 billion B2: $35 billion B3: $79 billion

Starting from the original initial balance, fill out the missing entries to achieve those snapshotted balances. (There may be more than one valid answer for each entry.)

Who starts the snapshot: B2 
Event right before B2 starts snapshot:

Event right before B1 receives B2 marker:

Event right before B1 receives B3 marker:

Event right before B2 receives B1 marker:

Event right before B2 receives B3 marker:

Event right before B3 receives B1 marker:

Event right before B3 receives B2 marker:

1.5 GDB’s engineers have been considering making some changes to the algorithm. Each question below describes a modification they would like to add to the Chandy–Lamport snapshot algorithm. For each variation, explain whether the snapshot is still guaranteed to be consistent.

- After recording its local state, a branch B_i sends a marker on each outgoing channel and closes all incoming channels immediately after sending the marker.

- Channels guarantee no messaging order, i.e. they are not FIFO.

- A branch waits to record its local state and incoming channels’ states until it has received markers from two different incoming channels, instead of the first marker.

# Question 2

In the following Paxos trace, P1, P2, P3 are proposers and A1, A2, A3 are acceptors. At the beginning of the trace, each acceptor’s acceptedProposal and acceptedValue are null. Each step indicates that a message is sent at a given time. You may infer that a message arrives by the existence of a response (or blank) that depends on an earlier message.

Consider the following trace:

![[Distributed Systems-1.png]]

2.1 Fill in the blanks of the trace so that each acceptor makes each promise and accepts each proposal if it is able; an acceptor rejects a promise or proposal only if necessary.

`____(1)____`:


`____(2)____`:


`____(3)____`:


`____(4)____`:

`____(5)____`:

`____(6)____`:

2.2 In this trace, what (Proposal number, Value) pairs have been accepted by any of the acceptors? (select all that apply, even if the value is not eventually chosen)
- [ ] (10, V1)
- [ ] (20, V1)
- [ ] (10, V2)
- [ ] (30, V1)

2.3 By the very end of the trace, what proposal number and value has been accepted by all acceptors?

2.4 After which step does a proposer first have enough information to know that a value has been chosen by a majority of acceptors? Identify the step and explain why.

2.5 Assume that a proposer has been taken over by an adversary. How can this proposer ensure the algorithm violates liveness by following the rules of the protocol?

# Question 3
Yuvraj and Srini want to discuss the final exam questions through email. They decided to encrypt their emails to avoid being attacked by genius students like you. The first thing they have to do is to agree on a secret key. A TA suggests that they can use Diﬃe-Hellman key exchange protocol.

3.1 Suppose they have agreed on public values g = 5 and p = 23. Yuvraj chooses his secret number a = 6, and Srini chooses his secret number b = 8. What value should Yuvraj send to Srini? What value should Srini send to Yuvraj? What is the shared secret key they agree on?

3.2 Assuming they use cryptographically secure primes, why can the final exam questions still be stolen by an attacker? Give an example of an attack using the parameters from part 1.

3.3 What is the fundamental problem of this protocol (i.e. what security property is missing)? What diﬀerent protocol or variation in this protocol can protect the final exam?

3.4 Suppose Yuvraj and Srini decide to send their traffic through TOR instead of relying on regular Internet routing. What is one benefit and one drawback of using source routing in TOR versus regular routing on the Internet? Explain why.

# Question 4
Stephen is considering using RAID-to store data for his company. For this question, assume all disks have a capacity of 1500GB, MTTF of 7 years, read throughput of 500MB/s, and write throughput of 400MB/s.

Suppose Stephen buys 8 disks. He wants to use all 8 disks to build either RAID-0 or RAID-1 with a mirroring level of 4. Assume that disk failures are independent and exponentially distributed as presented in lecture.

4.1 What is the ratio of the read throughput of RAID-0 to the read throughput of RAID-1? That is, what is the value of (read throughput of RAID-0) / (read throughput of RAID-1)? Explain your answer.

4.2 What is the ratio of the write throughput of RAID-0 to the write throughput of RAID-1? Explain your answer.

4.3 What is the ratio of the MTTDL of RAID-0 to the MTTDL of RAID-1? Give your answer up to 2 decimal places.

4.4 What is the maximum number of disk failures this RAID-1 array can tolerate? Enter just the number, no spaces or other words.

# Question 5
RAID-50 is a composite RAID configuration. You can think of it as a RAID-0 array of RAID-5 subarrays. Observe the following diagram for the configuration we will be using in this question.

You have 8 total disks at your disposal. For the RAID-50 you will be working on, you have 2 individual 4-disk RAID-5 subarrays. See the diagram below. We will use one disk’s worth of space for parity blocks for each RAID-5 subarray.

![[Distributed Systems-2.png]]

5.1 If the read throughput of an individual disk is 100 MB/s, what is the maximum read throughput of the 8 disk RAID-50 array? Simplify your answer into a single number and unit.

5.2 If the write throughput of an individual disk is 70 MB/s, what is the maximum write throughput of the 8 disk RAID-50 array? Assume for this question that read and write throughputs are equal, and that all writes are small random writes rather than a full-striped write. Simplify your answer into a single number and unit.

5.3 If the MTTF of a single disk is 8.000 years, what if the MTTDL of the 8 disk RAID-50 array? Simplify your answer into a single number (round to 3 decimal points) and unit. Show your work for partial credit.

# Question 6
For the following comparison questions assume an 8 disk array. RAID-4 will have 1 parity disk and 7 data disks, and RAID-5 will have 1 striped/rotating parity disk and 7 data disks.

### Q6.1 6.1

Which of the following would you choose to solely maximize reliability (expected MTTDL) if you had an 8 disk array?

Choice 1 of 5:RAID-0
Choice 2 of 5:RAID-1 with mirror level M of 4
Choice 3 of 5:RAID-4
Choice 4 of 5:RAID-5
Choice 5 of 5:RAID-50 as described above



### Q6.2 6.2

Which of the following would you choose to solely maximize effective capacity (logical capacity) if you had an 8 disk array?


Choice 1 of 5:RAID-0
Choice 2 of 5:RAID-1 with mirror level M of 4
Choice 3 of 5:RAID-4
Choice 4 of 5:RAID-5
Choice 5 of 5:RAID-50 as described above


### Q6.3 6.3

Which of the following would you choose to maximize read throughput AND have some level of reliability if you had an 8 disk array? Select all

Choice 1 of 5:RAID-0

Choice 2 of 5:RAID-1 with mirror level M of 4

Choice 3 of 5:RAID-4

Choice 4 of 5:RAID-5

Choice 5 of 5:RAID-50 as described above

### Q6.4 6.4

Which of the following would you choose to **minimize write latency** AND have some level of reliability if you had an 8 disk array?

Choice 1 of 5:RAID-0
Choice 2 of 5:RAID-1 with mirror level M of 4
Choice 3 of 5:RAID-4
Choice 4 of 5:RAID-5
Choice 5 of 5:RAID-50 as described above

### Q6.5 6.5

Your company is limited on funds. You decide to tell Scotty to pick whichever RAID-array is best at “both capacity and write throughput” while having some reliability. In other words, which of the following would you choose to **maximize** the product of **write throughput and capacity** AND have some level of reliability if you had an 8 disk array?

Question 6.5 answer field

Choice 1 of 5:RAID-0
Choice 2 of 5:RAID-1
Choice 3 of 5:RAID-4
Choice 4 of 5:RAID-5
Choice 5 of 5:RAID-50 as described above