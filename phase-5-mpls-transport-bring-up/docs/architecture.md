# Phase 5 Architecture

## Transport model

The SD-WAN fabric uses two transport colors:

- `mpls`
- `public-internet`

The objective of Phase 5 is not to replace the existing Internet transport, but to make the MPLS path equally usable by the SD-WAN control plane and by BFD.

## OSPF extension

OSPF already existed in the MPLS core from Phase 1. Phase 5 extends that reachability toward the vEdges and standardizes relevant WAN links as point-to-point.

For vEdge-PRS2:

- system IP: `55.55.55.51`
- MPLS interface: `ge0/0`
- MPLS address: `50.1.2.1/24`
- OSPF peer observed: `50.1.2.2`
- neighbor router ID: `2.2.2.4`

## MPLS ↔ Internet interconnect

Internet Router and MPLS-P3 are connected through:

- Internet Router: `3.3.3.1/30`
- MPLS-P3: `3.3.3.2/30`

Both sides use OSPF point-to-point.

This link allows each transport domain to learn the other's transport prefixes, which is what enables cross-transport BFD combinations such as MPLS→Internet and Internet→MPLS.
