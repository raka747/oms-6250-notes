# linkin' hosts with switches

- host has LAN/MAC/Physical addy
- sends a datagram with a "dest" header
- can send a "broadcast", too
- host may know the IP of another machine, but not the h/w address
    - how to learn?
    - ARP! Address Resolution Protocol
        + host queries to all nodes (broadcast)
            * "who has this IP address? 1.2.3.4"
            * response come from host who has that addy, response has MAC
        - host builds table of IP/MAC addresses
+ host encapulates IP packet in "wrapper" e-net packet

* hubs broadcast incoming packets on all outbound ports
    * yey, hosts connected
    * booo! flooding, frame collision, misconfigured device

* switches - partition the shit show made by hubs
    - intelligently does _not_ broadcast to each LAN segment
    - switches have to map DEST MACs to Switch ports!
        + LEARNING SWITCH does this automatically
            * first, table empty, and floods everyone on first packet send
            * sees where first frame came from. maps host desitination to physical port
            * sniffs all traffic, and detects which host responds, and maps host to port
    - some switches have redundancy, introduce cycle/flood risk
        - broadcast on "spanning tree", which is a tree where no node in the graph is cycled
* how big should buffers be on a switch line?
    - 2*T*c, where c is capacity of bits of the line bottleneck
