# e2e argument in sys design

[@link](http://web.mit.edu/saltzer/www/publications/endtoend/endtoend.pdf)

## technical jargon-ridden arg

"The function in question can completely and correctly be implemented only with the
knowledge and help of the application standing at the end points of the communication
system. Therefore, providing that questioned function as a feature of the communication
system itself is not possible. (Sometimes an incomplete version of the function provided
by the communication system may be useful as a performance enhancement.)"

## practical example - file transfer
- to xfer a file machine to machine is subject to many failures
    + host A file read errors, buffer, packetize, network send, host b recieve, host b write
    + adding strict resilency to each step may not be practical, or feasible
    - instead, "end-to-end check and retry". e.g. do it all, assuming no error, and test checksums
    - "the application program that performs the transfer must supply a file-transfer-specific, end-to-end reliability guarantee"

## performance
- clearly some level of low level checks need to happen, as some systems have known unreliability
    + dont over do it though, e2e checks still need to be performed
- don't justify low level performance always if:
    + applications that do not need the function will
pay for it anyway
    + the subsystem may not have as much information as the
higher levels, so it cannot do the job as efficiently
        - ex if each packet relay in a network does checking and error detection, some apps that care more about speed than correctness had no say, and suffer

## application of rule
(many examples given)

- phone conversation.  application is a dialogue between two people.  e2e applies, as perf is critical, and resiliency/lossiness is not.  a person can ask for something to be repeated.
    - phone recording?  nature changes completely.  person to machine can't have that "hey repeat that" opporitunity (play along, ok), so now, e2e principles may apply less, and the resiliency of the mediums become critical.
    - performance vs resiliency