---
title: IPv6 Address Space for Space
abbrev: IP Space for Space
docname: draft-limarsjenwar-tiptop-address-space-00
category: std

ipr: trust200902
area: General
workgroup: TIPTOP Working Group
keyword:
  - IPv6
  - Deep Space
  - Address Allocation
  - IANA
  - Aggregation

stand_alone: yes
smart_quotes: no
pi: [toc, sortrefs, symrefs]

author:
  -
    ins: R. Atkinson
    name: Ran Atkinson
    email: rja.lists@gmail.com
  -
    ins: M. Eubanks
    name: Marshall Eubanks
    org: Space Initiatives
    email: tme@space-initiatives.com
  -
    ins: W. Kumari
    name: Warren Kumari
    org: Google, Inc.
    email: warren@kumari.net
  -
    ins: T. Li
    name: Tony Li
    org: Hewlett Packard Enterprise
    email: tony.li@tony.li
  -
    ins: J. Linkova
    name: Jen Linkova
    org: Google, LLC
    email: furry13@gmail.com

normative:
  RFC2119:
  RFC8174:

informative:
  RFC1518:
  RFC1881:
  RFC8720:
  I-D.many-tiptop-ip-architecture:

--- abstract

IP communication in space environments is fundamentally different from terrestrial communication; a primary difference is the likelihood of long round-trip times, potentially minutes or even hours, depending on the distance between the endpoints.

Existing protocols and IP stacks are largely designed for low-latency terrestrial environments and may fail (e.g., standard TCP handshakes timing out) unless they can readily identify that communication is taking place with a peer in a space environment and adjust their behavior accordingly. Furthermore, without a structured address allocation plan, early space missions risk creating an unaggregated patchwork of prefixes—repeating the historical operational scaling issues seen in terrestrial networks.

This document requests that the IANA allocate a single dedicated block of IPv6 address space specifically for use in space environments and manages suballocations from that block for celestial bodies, as needed.
The Number Resource Organization (NRO) will determine how to allocate and assign address resources from the celestial bodies blocks, with the understanding that topological address aggregation is critical for routing scalability and operational efficiency.

--- middle

# Introduction

The exploration and operational utilization of outer space depends heavily upon reliable communications infrastructure and increasingly relies on the Internet Protocol suite {{I-D.many-tiptop-ip-architecture}}.

However, IP communication in space environments is fundamentally different from terrestrial communication. For example, the speed-of-light round-trip time (RTT) between Earth and Mars ranges from roughly 6 minutes to over 40 minutes. Traditional interactive transport connections (such as standard TCP handshakes and conservative retransmission timers) fail in these high-latency, intermittently connected environments. For an IP stack or application to know that a given flow requires specialized transport parameters, timer adjustments, or delay-tolerant convergence protocols, it needs a reliable, lightweight mechanism to determine that the remote destination resides in a space environment.

By establishing a dedicated block of IPv6 address space specifically for space environments, endpoint IP stacks and intermediate gateways can immediately identify when traffic is bound for deep space and adjust their behavior accordingly.

Additionally, addressing in space must be structured proactively to avoid the routing fragmentation that has historically plagued terrestrial networks. In the early days of IPv4 prior to the adoption of Classless Inter-Domain Routing (CIDR) {{RFC1518}}, address space was handed out in a disjointed manner, creating a sprawling, unaggregated global routing table colloquially referred to as "the swamp." If addresses for space missions continue to be assigned ad-hoc on a per-mission basis, the resulting patchwork will prevent route aggregation and impose severe routing table overhead on resource-constrained space hardware.

This document requests that the IANA allocate a single dedicated block of IPv6 address space for space environments, and charges the Number Resource Organization (NRO) with determining how to allocate and assign address resources from this block, ensuring that topological aggregation remains a primary design requirement.

# Conventions and Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 {{RFC2119}} {{RFC8174}} when, and only when, they appear in all capitals, as shown here.

# Routing Scalability and Topological Aggregation

Address aggregation allows the combining of multiple topologically related address prefixes into a single, less-specific route advertisement. Carrying fewer prefixes in routing and forwarding tables minimizes protocol overhead, conserves memory, and saves router CPU cycles—all resources that are at a premium on spaceborne systems.

To design an effective aggregation architecture, address plans must reflect the physical topology of the network. Terrestrial Internet topology shows dense connectivity on land masses where links are relatively inexpensive and simple to deploy, interconnected by a smaller number of long-distance transoceanic conduits. By analogy, communications infrastructure in space will exhibit high density within local environments (such as on and around individual celestial bodies) and far sparser links across interplanetary distances.

Consequently, route aggregation is most naturally and effectively performed around celestial bodies.
Within the dedicated space address block, dedicated blocks are suballocated for celestial bodies, as needed.
Address assignment policies MUST prioritize topological aggregation at the celestial body level, and, whenever possible, hierarchically below (e.g., local surface regions, orbital regimes, and localized operator constellations), ensuring that interplanetary transit gateways need only advertise and route coarse summary prefixes.

# Address Administration and Allocation Model

Administration of space IPv6 resources should build upon the established principles and operational expertise of the Internet numbers registry system {{RFC8720}}.

Under this model:

1. **IANA Allocation**: The IANA will allocate a single dedicated block of IPv6 address space for space environments. The IANA also manages suballocations for celestial bodies from that block.
2. **Registry Distribution**: The Number Resource Organization (NRO) will determine how to structure, assign, and distribute address blocks from the celestial bodies space allocations.
3. **Policy and Aggregation**: The registry system will establish allocation policies for space operators, network service providers, and research organizations, ensuring that address assignments preserve strict topological aggregation at the celestial body level and, whenever possible,  below.

Leveraging the existing registry framework allows the community to utilize proven policy development processes, governance structures, and well-understood allocation mechanisms, while ensuring that the physical and topological constraints of space routing are met.

Delegation of address space by the IANA is subject to standard stewardship principles {{RFC1881}}: if delegated space is mismanaged, the IANA retains the authority to revoke delegations in accordance with established registry operational guidelines.

# Security Considerations

Assigning a dedicated IPv6 block for space environments does not inherently introduce new security vulnerabilities to the IP architecture.
Additionally, some of existing routing security mechanisms might be unsuitable for space communications, while some others (such as boundary filterings) are still applicable.
Exact security mechanisms applicable for space environments are outside of scope of this document.

# IANA Considerations

This entire document relates to IANA numbering assignments.

The IANA is requested to allocate a single dedicated block of IPv6 address space specifically for use in space environments. (**TBA (furry@): /3?**)
The IANA is requested to suballocate /X (**we need to specify, I guess?) prefixes for the following celestial bodies:

* The moon and its environs.
* Earth's Lagrange points

When space communication is extended to other bodies not listed above, requests for sunsequent allocations will be made to the IANA.


The NRO will determine how to allocate and assign addresses from those blocks in accordance with the aggregation principles outlined in this document.

--- back

# Acknowledgments
{:numbered="false"}

The authors would like to thank Alejandro Acosta, Marc Blanchet, Kasey Kierra, Michael Richardson and many other members of the TIPTOP working group
for their feedback and suggestions on this document,
and for their work on the broader topic of IP communication in space environments.
In addition, the authors would sincerely like to thank Kim Davies, John Curran and Geoff Huston for helping us understand
the history, complexity and sensitivities around IP address governance.
We would also like to thank the members of the RIPE Address Policy Working Group for their feedback and suggestions
on this topic.  One of the authors (Warren) has an awful memory for
names and faces, and is embarrassed that he can't remember who all he spoke to about this topic, but he is grateful to everyone who
provided feedback and suggestions - please drop me a note and I'll be happy to add you to this list.

