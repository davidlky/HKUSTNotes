## 5. ICMP - Internet Control Message Protocol
- source sends series of UDP segments, first is TTL = 1 
    - TTL = Time to last
    - second has TTL = 2, etc.
    - unlikely port number
- when datagram in `nth` set arrives to `nth` router
    - router discards the datagram and sends source ICMP control message (type 11, code 0)
    - ICMP message includes name of router and IP address
- ICMP has v4 and v6 as well

## 5.7 Network management and SNMP
- 