---
title: "Address Space for Space"
category: info

docname: draft-kumari-tiptop-address-space-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: AREA
workgroup: TIPTOP
keyword:
 - space
 - address_policy
venue:
  group: WG
  type: Working Group
  mail: deepspace@ietf.org
#  arch: https://example.com/WG
  github: wkumari/draft-kumari-tiptop-address-space
  latest: https://example.com/LATEST

author:
  -
    ins: W. Kumari
    organization: Google, Inc.
    email: warren@kumari.net
  -
    fullname: Jen Linkova
    organization: Google, LLC
    email: furry13@gmail.com

normative:

informative:
  RFC1881:

...

--- abstract

{Editor note (To be removed before publication): The high-level summary of this
document is that the IANA allocates a block of IPv6 address space specifically
for use in space environments.

IP communication in space environments is fundamentally different from
terrestrial communication; e.g., the speed-of-light RTT from Earth to Mars
ranges from ~6 minutes to ~45 minutes, which means that traditional connections
(e.g Telnet over TCP) won't work. For an IP stack to know that a connection
will require special handling (e.g. adjusting timers, or using different
protocols), it needs to know that the latency to the remote peer is going to be
significantly higher than typical terrestrial latencies. By allocating a
specific block of IPv6 address space for use in space environments, IP stacks
can easily identify when they are communicating with a peer in space, and
adjust their behavior accordingly.

This document requests that the IANA allocate a block of IPv6 address space
specifically for use in space environments and then delegate from that block
to the existing RIRs. The RIRs can then set policies for address allocation and
assignment within the space address block and make address allocations to
their members from this block.

This approach leverages the existing RIR systems, including their policy
development processes, governance structures, and existing relationships with
their members. This includes relationships with governments within their
regions, thus bypassing many of the geopolitical issues, including dealing
with sanctioned countries, etc. The only real change is that the RIRs would be
allocating from a different block of addresses, and setting policies for that
block; the overall process would be the same as it is today. This is a much
simpler and more efficient approach than creating a new registry for space use,
or having a single RIR manage the entire space address block, along with all of
the geo-political issues that would entail.

WK: This editor note seems to actually be most of the document... :-) }

IP communication in space environments is fundamentally different from
terrestrial communication; a primary difference is the likelihood of long
round-trip times, potentially minutes or even hours, depending on the distance
between the endpoints.

Existing protocols are not designed for such environments and so may not work
as expected. For example, TCP connections will fail due to timeouts unless IP
stacks know that the remote peer is in space, and adjust their behavior
accordingly.

This document requests that the IANA allocate a block of IPv6 address space
specifically for use in space environments, and then delegate from that block
to Regional Internet Registries (RIRs) for space use.

The RIRs can then set policies for address allocation and assignment within the
space address block, and make address allocations to their members from this
block.


--- middle

# Introduction

In order to allow IP stacks to easily identify when they are communicating with
a peer in space, this document requests that the IANA allocate a block of IPv6
address space specifically for use in space environments.

The IANA will delegate from this block to Regional Internet Registries (RIRs)
the task of making specific address allocations for space use to network
service providers and other subregional registries.

The RIRs will then be responsible for setting policies for address allocation
and assignment within the space address block, and for making specific address
allocations to network service providers and other subregional registries.

Individuals and organizations may obtain address allocations for space use
directly from their appropriate RIR (or other) registry, or from their service
provider.

{Ed note: The text below is adapted from [RFC1881]. } Delegation of address
space by the IANA is not irrevocable. If, in the judgment of the IANA, a
registry has seriously mishandled the address space delegated to it, the IANA
may revoke the delegation, with due notice and with due consideration of the
operational implications. IANA will make every effort in such a case not to
revoke addresses that are in active use, unless there are overwhelming
technical reasons for doing so.

The definition of what constitutes "space use", the size of the block to be
allocated, and the policies for address allocation and assignment within the
space address block are outside the scope of this document, and are left to the
RIRs to determine. The RIRs are already responsible for setting policies for
address allocation and assignment within the existing IPv6 address space, and
so are well placed to set policies for the new space address block as well.

There are two primary approaches possible for how the IANA can delegate address
space for space use to the RIRs. {Ed note: The authors prefer the first
approach, as it is simpler and more efficient, but it does result in probably
2-5 prefixes per planet. While a single aggregate per planet would be nice,
5ish doesn't seem overly difficult to manage. Which approach to choose is of
course up to the WG / IESG, probably with input from the IANA as to complexity,
etc.}:

1. The IANA can delegate a single large block for space use, and RIRs can
request large blocks from that block as needed. The RIRs can then designate
sub-blocks for different planetary bodies and allocate from those sub-blocks as
needed. This does mean that there will be more than one prefix per planet -
probably up to five (the number of RIRs). If an RIR were to exhaust their
allocation for a particular planet, they could request more from the IANA, or
recarve their existing allocations, but this seems unlikely given the size of
the block that would be allocated.


2. The IANA can delegate a separate block for each planetary body, and then
delegate from those blocks to the RIRs as needed. This would mean that there
would be a single prefix per planet, which may be desirable for operational
reasons, but it does mean that the IANA would need to make multiple
delegations, the RIRs would need to manage multiple blocks, and the address
allocation would be significantly less efficient, as each block would need to
be large enough to accommodate the future needs of all RIRs for that planet,
which may be difficult to predict.


# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations

TODO Security


# IANA Considerations

This entire document is an IANA considerations document.

The IANA is requested to delegate a block of IPv6 address space specifically
for use in space environments, and then allocate from that block to RIRs for
space use.

{Ed note: This document does not specify the size of the block to be delegated
for space use, nor what size blocks to delegate to each RIR as needed - this is
left to the IANA to determine. The authors (and WG) will be happy to provide
input on this if the IANA would like, but ultimately this is a matter for the
IANA to decide.}

--- back

# Acknowledgments
{:numbered="false"}

The authors would like to thank the members of the TIPTOP working group for
their feedback and suggestions on this document, and for their work on the
broader topic of IP communication in space environments. In addition, the
authors would sincerely like to thank Kim Davies, John Curran and Geoff Huston
for helping us understand the history, complexity and sensitivities around IP
address governance. In addition, we would like to thank the members of the RIPE
Address Policy Working Group for their feedback and suggestions on this topic.
One of the authors (Warren) has an awful memory for names and faces, and is
embarrassed that he can't remember who all he spoke to about this topic, but he
is grateful to everyone who provided feedback and suggestions - please drop me
a note and I'll be happy to add you to this list.
