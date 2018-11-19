## Link Layer
- hosts and routers are nodes
- communication channels between nodes - links
    - do not differentiate between the nodes, only care about nodes
    - wired, wireless, LAN etc.
- layer-2 packet: frame, encapsulate the datagram
- data-link layer worries about the transferring datagram from one node to physical adjacent node over link

Context
- datagram transferred by different link protocol over different links
    - Ethernet, then frame relay, 802.11 last
- Each link protocol provides a different service
    - like train -> plane -> train -> car

Link Layer Services
- framing and link access
    - encapsulate datagram into frame, add header, trailer
    - channel access if shared medium (shared wiring)
    - "MAC" address in header for source and destination
        - different from IP

- reliable delivery between nodes
    - usually not needed for the low bit-error links (fiber, twisted pairs etc)
    - wireless links: high error rates
        - should you have link-level reliable deliver?
            - arguable here, should you spend resource on this?