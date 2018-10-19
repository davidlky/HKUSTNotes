## Transport Layer

### Transport Layer Services
- logical communication between app processes running on different hosts
- run on end systems, protocols:
  - send side: break app messages into segments, pass to network layer
  - receiver side: reassembles segment into messages, passes to app layer
- 2 protocols: UDP and TCP

Transport vs Network Layer
- Network Layer: logical communication between hosts (the next layer)
- Transport Layer: logical communication between processes
  - depends on and enhances network layer services

TCP: in-order, reliable delivery
- congestion, flow and connection control

UDP: unreliable, unordered, "best-effort"

Neither has delay guarantees or bandwidth guarantees

### Multiplexing/De-Multiplexing
- multiplexing at sender: handle data from multiple sockets, add transport header
- de-multiplexing at receiver: use header info to deliver segment to proper socket
  - host receives a datagram
    - has 32 bits (source port, dest port)
    - has source/dest IP address
    - "transport layer segment"
  - host use IP addresses and port numbers for correct socket for app layer

Connection-less De-Multiplexing (UDP)
- only cares about dest port + IP
- socket has host-local port #
- when host receives UDP segment, check port # and direct
  - same dest + port # but different source will be directed to same socket

Connection based Demux (TCP)
- 4 tuples (source/dest ip/port)
- use all 4 values
- web servers have different sockets for each connecting client
  - non-persistent will have different socket for each request
  - the server can be threaded

### Connection-less Transport (UDP)
- UDP -> User Datagram Protocol (RFC 768)
- connection-less = no handshaking, each segment independently handled (no state)
- streaming, DNS, SNMP
- add reliability at application layer

Segment Header
- port numbers, length (length including header, in bytes), checksum and then payload
- benefits of UDP
  - small header size
  - no congestion control - fast
  - fast in general

Checksum
- goal: detect errors (flipped bits) in transmitted segments
- sender: treat contents and header as sequence of 16 bit numbers
  - checksum made by adding everything
- receiver:
  - compute checksum of segment, check if they equal
- use 1's compliment to break it up (flip at first 0, or just add a 1 at the end + flip after)

### Principles of Reliable Data Transport
- RDT -> reliable data transfer
- based off of UDT first
- rdt_send -> udt_send -> rdt_rcv -> deliver_data
- use FSM to illustrate, build it up. consider only unidirectional

rdt1.0
- assuming underlying udt is perfectly reliable
  - no bit error and no loss of packet
- FSM of the 4 steps (packing and unpacking) should be good
![image](Networks/images/3.png)

rdt2.0
- underlying channel may flip bits
- use checksum to detect errors
- how to recover from errors?
- ACK - tell sender the packet was good
- NAK -> say it has errors
  - sender will resend
- new: error detection + feedback control
- problem: what if ACK/NAK is corrupted?
  - cant retransmit: duplicate, need to add sequence number to each pkt
  - stop and wait (sender)

rdt2.1
- sequence number added to pkt (only 1 and 0 needed)
- check if ACK or NAK is corrupted
  - 2x state now, check if seq has 0 or 1
- must check if received packet is duplicate
  - receiver does not know if the last ACK/NAK is received properly at sender.

rdt2.2: NAK-free
- no more NAK, include seq # of pkt being ACKed
  - sends for last pkr received OK
- duplicate ACK at sender means NAK
  - retransmit current one

rdt3.0: channels with errors and loss
- if underlying channel can also lose packets
- sender wait a reasonable amount of time for ACK
  - retransmit if no ACK received (assume loss)
- requires a countdown timer
- even when duplicate, still send an ACK with segment number

- performance is bad, because you have to wait
  - network protocol limiting use of physical resources
- Utilization: fraction of time sender busy sending
  - `L/R / (RTT + L/R)` -> no pipelining

Stop and wait operation
- RTT is needed to see if a package has successfully been received.
  - RTT + L/R

Pipelined Protocols
- pipelining: allow multiple "in-flight", yet to-be-ack pkts
  - range of sequence number needs to be increased
  - buffering at sender/receiver

Go-Back-N
- sender: have up to N unacked packets in pipeline
- receiver: cumulative ack, no ack if there's a gap
- sender has timer for oldest unacked packet (when expire, send all unacked)
- window of N (consecutive unack'ed pkt)
  - cumulative ack (ack up to which n), has a timer for the oldest one
  - transmit n and higher seq packets in window
- receiver: ACK-only: always send ACK for correctly-received pkt with highest in-order seq #
  - may have duplicate ACKs, keep track of next seq num
  - out-of-order: discard, re-ACK pkt with highest in-order seq #
- waiting for timeout usually when things fail, as the timer is only kept for the last in-order one

Selective Repeat
- have up to N unack'ed pkt, individual ack for each packet
  - have timer for each one, transmit only that one on expire
- needs to buffer pkts, for eventual in-order delivery
- individual timer, resend only when un-acked
- window: N consecutive seq #, limits the amount sent and unACKed pkts


dilemma:
- when seq number and window are the same size, then possible to have duplicate data accepted as the new one.

### Connection Oriented Transport: TCP
- point to point (one sender, receiver)
- reliable, in-order byte stream
- pipelined
- full duplex data - bi-directional data flow
- connection oriented
  - handshaking, checking state before sending
- flow controlled: sender does not overwhelm receiver

Q: how to set TCP timeout value?
- longer than RTT (but it varies)
- too short: timeout early, unnecessary re-transmission
- too long: slow reaction to segment loss

Q: how to estimate RTT?
- `SampleRTT`: measured time from segment transmission until ACK received
  - will vary, want to estimate RTT smoother -> average several recent measurements, not just current RTT 

TCP round trip time, timeout
- EstimateRTT = (1 - a)*EstimateRTT + a*SampleRTT
  - exponentially weighted moving average
  - influence from past becomes less and less relevant
  - usually a = 0.125

- we need a safety margin for smoothing
  - large variation in ERTT -> larger safety margin
  - estimate SampleRTT deviation from EstimatedRTT
  - DevRTT = (1 - b) x DevRTT + b x |SampleRTT - EstimatedRTT| (b usually being 0.25)
  - TimeoutInterval = EstimatedRTT + 4 * DevRTT
- obviously still not perfect


### Reliable data transfer
- TCP creates `rdt` service on top of IP's unreliable server
  - pipelined segments
  - cumulative acks
  - single retransmissions timer
- retransmissions triggered by timeout or duplicate ack
  - duplicate ack is earlier than timeout and easily indicating something went wrong

Sender events
- data received from app:
  - create segment with #, start timer (oldest unacked segment)
  - expiration interval established
    - on timeout: retransmit segment that caused timeout, restart timer
  - ack received
    - if ack is for previously unacked segments: update what is known to be acked, start timer for unacked segments.
  - duplicate acks for when the packets arrived out of order, the duplicate ack will ask for the next one in order.
- detect lose segment via duplicate ACK -> sender often send many segments back to back
  - if lost, there will likely be many duplicates
- TCP fast retransmit
  - if sender receives 3 ACKs for same data -> resent unacked segment with smallest sequence, don't wait for timeout
- TCP rarely go to timeout (performance will be too poor if it does often)
  - timeout basically means nothing is received! way worse