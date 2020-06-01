## Relationship to Other WGs and RGs

This is an expanded version of the section of a similar name in the
proposed charter.  We'll develop this here and then make the needed
changes to the charter.

The objective here is to look at about a dozen other WGs and IRTF RGs
and agree what our technical relationship with them is going to be.

Note that the current version of this note does not address
interaction with other SDOs yet.

* To do: find out whether there we envision such interaction with
  other SDOs.

## Types of relationship

* "watch": shared interests, but no specific exchange or mutual dependency
envisioned now; could develop, though.
* "import": specs that the other WG works on will be used by ours.
* "export": we could do some work that would benefit that other WG.
* "consult": actively obtain input from the other WG (for watching or importing).

<!-- ## "Transport protocol" area of work -->

## Working groups, Research Groups

* Name: TCPM, TSVWG, QUIC, AVTcore
* Work: Transport protocol innovations
* Issue in other group: What new transport protocol mechanisms provide
  benefits that cannot be had with a classical transport
* **Issue in LOOPS**: Develop the retransmission part of LOOPS (as well as
  possibly the reconstruction/FEC part) based on these innovations
* Type: Watch, potentially Import
* **Issue in LOOPS**: Are there new interactions between the LOOPS
  "transport" elements and the innovations in the upper layer transport
  protocols?
* Type: Watch

---

* Name: TCPM
* Work: RACK
* Issue in other group: (from draft-ietf-tcpm-rack-08:) ... develop a
   new TCP loss detection algorithm called RACK ("Recent
   ACKnowledgment").  RACK uses the notion of time, instead of packet
   or sequence counts, to detect losses, for modern TCP
   implementations that can support per-packet timestamps and the
   selective acknowledgment (SACK) option.  It is intended to be an
   alternative to the DUPACK threshold approach [RFC6675] ...
* **Issue in LOOPS**: Does LOOPS need to rely on a sequence-preserving
  path for efficient loss detection, or can we use some of the RACK
  work for more time-based loss detection?  How do we translate the
  TCP features used by RACK into features that are available in LOOPS?
* Type: Watch, potentially Import

---

* Name: MASQUE (WG to be, recent BOF 2020-03-24)
* Work: Embedding proxied flows into QUIC and HTTP/3
* Issue in other group: "Congestion Control over Congestion Control in
  case of UDP or IP proxying", i.e., when the proxied flows are UDP or
  IP (~ VPN), the interaction between end-to-end transport protocol
  control loops (congestion control) and the control loops run by QUIC
* **Issue in LOOPS**: Does LOOPS need to perform specific work to mitigate
  issues stemming from nested congestion control?  Note that the LOOPS
  segment is typically, but not always, significantly shorter than the
  end-to-end path, which might be similar in a MASQUE situation.
* Type: Watch

---

* Name: RMCAT, AVTcore
* Work: Congestion control for media flows
* **Issue in LOOPS**: Interactions between upper layer congestion control
  schemes in use for media and those in use on the LOOPS path segment
* Type: Watch

---

* Name: IPPM, TSVWG
* Work: Formats and algorithms for measurement
* **Issue in LOOPS**: What IPPM-defined formats and algorithms for
  measurement can we usefully import into the LOOPS measurement system
* Type: potentially Import
* To do: What came out of the
  draft-ietf-tsvwg-tunnel-congestion-feedback work?

---
<!-- ## "Tunneling and encapsulation" area of work -->

* Name: NVO3, INTAREA, SPRING/6MAN; NWCRG
* Work: Tunnel encapsulation formats
* **Issue in LOOPS**: We need to follow the homes of tunneling protocols
  to which bindings are being defined, which depending on the choices
  of the WG may include NVO3 (Geneve), intarea (GUE, GRE), spring/6man
  (SRv6).  There also is some tunnel/encapsulation work done as part
  of NWCRG's work.
* Type: Import, consult

---

* Name: TSVWG
* Work: Advanced ECN
* Issue in other group: Agree on an approach for advanced ECN
* **Issue in LOOPS**: LOOPS can benefit from ECN both in the end-to-end
  traffic and in the LOOPS segment.
  The protocol may need to anticipate the developments on advanced ECN
  and adjust its usage of both classic and advanced ECN.  This may
  also influence how LOOPS makes use of RFC 6040 (Tunnelling of
  Explicit Congestion Notification).
* Type: Watch

---

* Name: DETNET, RAW
* Work: DETNET data plane, RAW, PREOF
* Issue in other group: Define a data plane (encapsulation) for
  replicating, eliminating duplicates, and potentially reordering
  traffic (PREOF).
  RAW extends this work to wireless networks.
* **Issue in LOOPS**: Can we integrate some of this work for
  retransmission and reconstruction?
* Type: Watch, potentially import
* **Issue in LOOPS**: Potentially (long term): Can we make some of the
  LOOPS components available in a way that is useful for DETNET and RAW?
* Type: Export

---

* Name: NWCRG (IRTF), TSVWG
* Work: FEC formats and protocols
* Issue in other group: Define forward error correction (FEC) formats
  that provide good robustness, low reconstruction latency, low
  implementation complexity, low CPU requirements, low overhead
* **Issue in LOOPS**: How does the structure of these new formats and
  protocols influence the way LOOPS handles reconstruction?
* To do: Watch the patent claim thickets in this space
* Type: Watch, Import/Reference (specific schemes)

---

* Name: MAPRG (IRTF), ICCRG (IRTF)
* Work: Measurement, Congestion control
* Issue in other group: Do leading edge work in this space
* **Issue in LOOPS**: Benefit from that leading edge work
* Type: Watch

---

* Name: PANRG
* Work: Path signaling
* **Issue in LOOPS**: In the long run, discovering LOOPS instances
  along the path as well as path characteristics inside the LOOPS
  segment might get interesting.
* Type: Watch, consult (at the right time)
