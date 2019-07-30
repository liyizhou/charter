# Charter proposal for a LOOPS WG, version 0.3.0

## Background

The Internet has a long history of employing performance enhancing
proxies (PEPs, RFC 3135) to improve performance over paths with links
of varying quality.  Today's PEPs often interact deeply and
"transparently" (intrusively) with end-to-end transport and
application layer protocols.  This practice is coming to an end with
increasing deployment of encryption.

At the same time, network structures are becoming more complex, and
network nodes are becoming more powerful.  It is becoming more viable
to trade processing power in network nodes against path quality, in
particular for expensive path segments.  Transport protocols and their
implementations are moving towards playing better with forwarding node
functions such as ECN marking and AQM.

## LOOPS

LOOPS (Local Optimizations on Path Segments) attempts to capture
opportunities opened by these developments, enabling optimizations
within segments of an end-to-end path.  Typically, these segments are
located between overlay nodes (tunnel endpoints), which allows a local
optimization protocol to run between these nodes.  Many end-to-end
flows can be aggregated into each such tunnel flow being optimized.

Initially, LOOPS will focus on path segments that do not include
either end host.  Also, multipath forwarding will not be specifically
addressed.  The functions to be addressed by LOOPS include:

* Local recovery.  Packet losses on the path segments are recovered
  autonomously, removing the need to burden the entire end-to-end path
  with the recovery, and decreasing the latency by which these
  recoveries can be effected.  Local recovery can be based on forward
  error correction (FEC) and/or (non-persistent) retransmission.

* Local measurement.  To properly parameterize the LOOPS algorithms
  (e.g., RTO, FEC rate), measurements are continuously performed of
  the path segment between the tunnel endpoints.

* Interaction with end-to-end congestion control.  Based on
  configuration and measurement information, losses can possibly be
  categorized into congestion and non-congestion losses.  The losses
  that cannot be positively identified as non-congestion losses are
  relayed as congestion events to the end-to-end congestion control.
  Circuit breakers (RFC 8084) may be employed on the LOOPS tunnel to
  further protect against congestion collapse.

The LOOPS protocol will need to run embedded into a variety of
tunneling protocols.  To this end, LOOPS will be defined on a generic
information model level, and initial bindings will be defined for a
small set of tunneling protocols to be selected by the working group.

## Initial scope

Initially, LOOPS will focus on a retransmission-only solution, the
"basic LOOPS protocol".  FEC support, as well as possibly additional
support components enabling host-to-network operation, are planned as
additional steps.

\[The IESG has to decide whether these steps can be chartered right
away or a rechartering is needed after delivering the basic LOOPS
protocol.]

## Relationship to IRTF RGs

Important groundwork for LOOPS was laid by ICCRG and NWCRG.  In
particular the documents of the latter will serve as a basis for the
FEC-based components of LOOPS.

## Relationship to Other WGs and SDOs

LOOPS will work closely with developments in TSVWG, TCPM, and in
particular with QUIC as an example of a transport protocol that may
more readily absorb features of interaction with LOOPS segments.
However, there is no dependency — LOOPS is designed to optimize
already in the presence of legacy transport protocols.
LOOPS will interact with the homes of tunneling protocols to which
bindings are being defined, which depending on the choices of the WG
may include NVO3 (Geneve), intarea (GUE), spring/6man (SRv6).
\[Add more here.  Any other SDOs?]

## Milestones

* LOOPS basic generic information model and protocol, WG document adopted,
  October 2019
* LOOPS basic generic information model and protocol, PS to IESG, May 2020
* LOOPS binding candidates identified and WG documents adopted,
  February 2020
* LOOPS binding to tunneling protocol A, PS to IESG, July 2020
* LOOPS binding to tunneling protocol B, PS to IESG, September 2020

* LOOPS support for FEC, WG document adopted, June 2020
* LOOPS support for FEC, PS to IESG, December 2020

* LOOPS support for host-to-network operation, WG document adopted,
  August 2020
* LOOPS support for host-to-network operation, PS to IESG,
  February 2021

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
    channel.  Depends on encapsulation.

* How to relay congestion for non-ECN-capable transports?
  * By dropping.  Or, actually, not even requesting a retransmission when
    a congestion event would need to be relayed anyway.

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

