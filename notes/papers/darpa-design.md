- Defense Advanced Research Projects Agency (DARPA)
- Datagrams (host-responsible delivery) not key in original TCP/IP proposals, later critical

## goal

dev "effective technique for multiplexed utilization of existing interconnected networks"

multiplexing strategy:
  - packet-switching (already integrated in ARPANET, prior DARPA network project)
  - circuit switching (no remote login sppt :( )

individual networks > gateways (internet packet switches) > individual networks
    - gateways use store and forward algos

## requirements (sorted by priority)
- support lossy transmissions (if bad guys cut ur cables)
- mutltiple types of communications sppt
- accodmate variety of networks
- permit distributed management of resources
- cheap.
- ease of access (low effort host addition)
- "resources must be accountable"

### how to sppt lossy
- replication of xfer state node to node
- fate-sharing (chosen strategy)
    - only the host maintains state of the xfer
    - intermediaries are stateless
    - weakness: internet doesn't report out on it's error

### tcp - first implmentation
- generic in nature
- "reliably sequenced data stream"

but...

- too reliable for XNET, which should work in unreliable conditions
- realtime apps
    - most delay comes from reliablity pieces (e.g. packet order sync)
    - missing a packet is _ok_, hence UDP :)

## lack of cost effectiveness
- "the headers of Internet packets are fairly long (a typical header is 40
bytes), and if short packets are sent, this overhead is
apparent. The worse case, of course, is the single
character remote login packets, which carry 40 bytes of
header and one byte of data.  At the other extreme, large packets for file transfer, with
perhaps 1,000 bytes of data, have an overhead for the
header of only four percent.

- retransmission of lost packets. Since Internet does not
insist that lost packets be recovered at the network
level, it may be necessary to retransmit a lost packet
from one end of the Internet to the other. This means
that the retransmitted packet may cross several
intervening nets a second time, whereas recovery at the
network level would not generate this repeat traffic.

# implementing a protocol in the net

"This, in turn, means that to
understand the service which can be offered by a
particular implementation of an Internet, one must look
not to the architecture, but to the actual engineering of
the software within the particular hosts and gateways,
and to the particular networks which have been
incorporated."

"A typical implementation
experience is that even after logical correctness [of a internet protocol] has
been demonstrated, design faults are discovered that
may cause a performance degradation of an order of
magnitude. Exploration of this problem has led to the
conclusion that the difficulty usually arises, not in the
protocol itself, but in the operating system on which the
protocol runs. This being the case, it is difficult to
address the problem within the context of the
ACM SIGCOMM -7- Computer Communication Review
architectural specification"

## tcp design history
- regulate bytes or packets?  bytes.
    + inject control flow information into the bytes, so control and data would be ACK
        + boo. abandoned
    - packets could be resized if the net had bottleneck
    - group to-be re-tranmismitted packets into a big packet
        + sometimes a host would send a gazillion, tiny 1 char packets, and the receiver couldn't process. so, re-trans was often required.  but, if the re-trans were all tiny still, the same issue would occur
- "the correct design decision may have been
that if TCP is to provide effective support of a variety
of services, both packets and bytes must be regulated, as
was done in the original ARPANET protocols"