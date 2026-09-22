



**R0**
Default, External
172.16.12.0/24, R1
172.16.12.1/24, R3

**R1**
Default, R0
172.16.12.01000000/26, S3
172.16.12.00000000/26, R2

**R2**
Default, R1
172.16.12.0/27, S1
172.16.12.00100000/27, S2

**R3**
Default, R0
172.16.12.10000000/27, S4
172.16.12.10100000/27, S5

**R4**
172.16.12.**101**00000/27, S
172.16.12.**100**00000/27, R1


**R1**
Default, R0
172.16.12.**100**00000/27, R2
172.16.12.**001**00000/27, R2
172.16.12.**11**000000/26, S3

**R2**
Default, R1
172.16.12.**100**00000/27, S1
172.16.12.**001**00000/27, S2

**R3**
Default, R0
172.16.12.**000**00000/27, R4
172.16.12.**101**00000/27, R4
172.16.12.**01**000000/26, S6

**R4**
Default, R3
172.16.12.**000**00000/27, S4
172.16.12.**101**00000/27, S5



Assume that there is one router between the links from Alice's computer (A) to Bob's computer (B). As depicted below, link1 has 200Mbps capacity, and link2 has 100Mbps capacity. The RTT between A and B is 1s, assuming trip times are symmetrical in both ways. Data from A to B needs to be broken into 10Kbit packets. Encryption and decryption are done on a per-packet basis and can be done in parallel with the networking (e.g. transmission, waiting). The encryption speed on Alice's computer is 1Gbps. The decryption speed on Bob's computer is also 1Gbps.

![q7_2.png](https://production-gradescope-uploads.s3-us-west-2.amazonaws.com/uploads/text_file/file/990893588/q7_2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIAV45MPIOWWUU5XUL4%2F20260922%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260922T001437Z&X-Amz-Expires=10800&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEND%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC1kJIuilYlI1LZG%2B2lnmNXfS4ttgSpMlfo6E50NbwYEQIgaMHCClW3ygLsbh0AEsoleh0K7w2dTp5qe3MImFIvjcgqxAUImf%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw0MDU2OTkyNDkwNjkiDJueL6SXRS3YFUCxlSqYBRZAxibsq8vYZEm6LadBTNoFI9IIrBJwxeKV6HWxBNoF3gpSZvMzjbseaa603Ejz62FYLFKFpQZYjzfwXaQjVhGnEkdcb%2BgDiN1pnjAgcPP8o3Bu0x5dYZVvIbbwn8HqyAy0zr5ZQmbBbzo3pyMX1aooqStFj5jAGPoEL3D4dHPrmh27FSCvWwBXyl0wqnNxKa%2FhOZZGeVOsNvvrA27dPSAbtQIDywRyANg5EW1XXudkwKTm%2F3ZWqkk1sUTarQO2pVBJlDbKlscZN%2BC5h38G3fNijoLm147QWaK8AuePtZ63aFJVf2kFJkiNZN7pxq2p1Ju4%2BocYg2g7GuIKlwMHthpgBAV2Jyb7%2BCP%2FqMLsvkci1ELCIrw0fuJqz42Ge0Yp7fhVIG5U0eDgh4isIqrMtNguJIOTe%2FxxzJaqYeYQLUCOH6W9wLWKgoIuqpWEP8uqP0UcpW4H4i%2F4w2YVcuqbYS0M%2BqBmi4tfWtu0qQ0WB7kg30C1YEcbHYAAooYl92eKAPR0f7ScNtIlfLO8KeKcC97E0YtVeZa%2FGyBPMrdT6AzMz%2F1ItpEjBYuC3A6lWNVcnDXmDBAX6XisWZDvzBbI7Qp%2FK3iFGSKaJBU2%2Fqrq%2BXh%2FexOV9EZ%2FzgDn43fRbn9GXbqqfj2bmCSgHfwfqxcHRPdr9TnAjeUhW6IJWnrD8px22wBJyYpeYvObLOyWBJByveglkmKlFG3q4Sri%2FOfwVceGZEIarp95TJtqfflL1XKpsDwlgqSiDjZkArq4L%2BCN2lv%2FleA8q6BFn7l4feNcl9GDW10Ss0n8UjFpyZXKkef%2BDmk51%2FKfeLgA0a2loDf0tTVimIecOwE4uk%2FlQ2T9IQmN8zeBkhlKhA0tuFff03wU05hLA7ryeuAwgoPH1QY6sQHqvnqs1gxwTpAw68Fh0rMaD94m97arK6AXN1rMZW13EWCyLt6n4DUifkxWNcs%2FHm6NgXYOACPdlJ62LUDPsVRwlBEpGAyjtzmMvqs4x1uUz5g0eF%2FeJM66gDrPcRhDZfbTzXuATBkyoS7EUkdCrzs9D5Be2mCUfoTaJ3cR6UQK9dp5hHck1mtqiovBayKXIQtS%2FCCZ6dMhj%2FzQgELYutNQnTlaNHakGjOwJwlcpGaW0xM%3D&X-Amz-SignedHeaders=host&X-Amz-Signature=4d13bee4adfad7e68fe0ba720f1a4a56b7147f466d355c1aafbabfd55dbe8fc7)

Round all answers to the nearest 10⁻⁵ (5d.p.).

Question 8.1

### Q8.1

2 Points

Grading comment:

Alice wants to send a secret file to Bob. How long does it take for Alice to send a 1Gbit secret file to Bob (one-way delay including the encryption and decryption time)? Assume Alice transmits continuously and Bob sends no ACKs. Give your answers in seconds and follow the precision rules above.

_Hint: The transmission delay is the time it takes to put a packet on the physical link, given by (packet size)/(link speed)._

10.50007 s

Save Answer

Question 8.1:

Last saved on **Sep 21 at 9:42 PM**

Question 8.2

### Q8.2

3 Points

Grading comment:

Alice, however, is not sure if Bob has received all the packets. She decides to use the stop and wait protocol to ensure the correct delivery of the packets. In this setup, Alice waits until she receives an ACK for the previous packet before transmitting the next packet. Assume that none of the packets are dropped, lost, or corrupted. You can also assume no encryption or decryption in this setup and there is no **transmission delay** for the ACK reply.

Compute the total time taken to transfer the entire file. Give your answers in seconds and follow the precision rules above.

Grading comment:

What is the effective bandwidth of this protocol (in Kbps)?

Save Answer

Question 8.2:

Question 8.3

### Q8.3

5 Points

Grading comment:

Alice soon realizes the protocol used above takes a long time to transmit the files because of poor bandwidth utilization. Note that Alice still needs to receive ACKs for the individual packets (cannot be cumulative). Assume that none of the packets are dropped, lost, or corrupted. You can also assume no encryption or decryption in this setup and there is no **transmission delay** for the ACK reply.

Suggest modifications to the protocol to improve bandwidth utilization.

Grading comment:

Suppose each host has a 100Kb network buffer, meaning at most 10 packets may be unacknowledged at any time. Compute the effective bandwidth in this case (in Kbps).

Grading comment:

Does your answer to the above question make sense? Explain the intuition.







Q3:

P1 P2 P3
each process uses unique pid (1, 2, 3) to calculate timestamp

T(p) = 10 * L(p) + id 
- L(p) is process current Lamport clock
- id acts as tie-breaker

- Delay: 2 steps to be delivered (received at t+2 where t is send time)
- Critical section duration: 3 steps
- Reply latency: can send no earlier than t + 1
- Action ordering: if must perform send AND receive, send always comes first
- Tie breaking for concurrent message arrival: lower process ID first
- Tie breaking for concurrent message departure: lower PID first
- Queue:
	- remove from queue at the SAME real time step it sends OK
	- Removes its OWN request from queue at the same step it starts critical section work
- No lost messages

Actions:
- B roadcast
- R eceive
- S end
- ExecCS
- ExitCS

Lp1 = 4, Tp1 = 41
Lp2 = 7, Tp2 = 72
Lp3 = 11, Tp3 = 113

