# Discussion

* So this is only about encrypted traffic?
  * Any traffic is welcome, we just don’t try to base this on peeking
    beyond L3 info.

* How do you know which packets are worth recovering?
  * Today we don’t.  If more L3 marking were to become available, we’d
    use it.

* How do you transport your measurement-related information?
  * Forward info: In encapsulation extension (e.g., with sequence
    number).   Reverse info: The same way we transport the ACK
    channel.  To be defined with encapsulation.

* How to relay congestion for non-ECN-capable transports?
  * Right now, we are only addressing ECN-capable end-to-end flows.
    But the answer in the future will have to be: By dropping.
    Or, actually, not even requesting a retransmission when a
    congestion event would need to be relayed anyway.

* How do you avoid spending more for LOOPS encapsulation than the
  performance enhancement is worth?
  * LOOPS will need some management that is weighing this (and doing
    the pair setup in the first place).

* How can you be better than bespoke satellite PEPs?
  * We can't, but we may be able to improve other path segments on the
    same paths of satellites.  We may also be good enough.

* Why don't you do multipath, optimization across several LOOPs pairs
  on the path, involve end hosts?
  * Crawl before walk; all of these are potential topics once a first
    version of basic LOOPS is delivered.  For now, it seems
    host-to-network operation is a high-priority next step.

