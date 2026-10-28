# Observed Transport State

## MPLS-P3 OSPF

`show ip ospf neighbor`:

| Neighbor ID | Address | Interface | State |
|---|---|---|---|
| 3.3.3.3 | 3.3.3.1 | Ethernet0/2 | FULL/- |
| 2.2.2.1 | 6.6.6.1 | Ethernet0/1 | FULL/BDR |
| 2.2.2.4 | 8.8.8.2 | Ethernet0/0 | FULL/DR |

The `3.3.3.3` adjacency confirms that MPLS-P3 and Internet Router successfully formed OSPF adjacency over the new interconnect.

## Internet Router OSPF

`show ip ospf neighbor` showed:

- `2.2.2.3` at `3.3.3.2` on `Ethernet2/1`: **FULL/-**
- `1.1.1.0` at `100.2.1.1` on `Ethernet0/0`: **FULL/DR**

## vEdge OSPF verification

Preserved Phase 5 device verification shows FULL OSPF adjacency on the MPLS-facing interfaces for:

- vEdge-DRC-Cyber2
- vEdge-DC-DCI
- vEdge-PRS1
- vEdge-PRS2
- vEdge-PRS3
- vEdge-LDN1
- vEdge-LDN2

## vEdge-PRS2 routing

Observed OSPF routes included:

- `3.3.3.0/30`
- `20.1.1.0/24`
- `20.2.1.0/24`
- `30.1.1.0/24`
- `30.2.1.0/24`
- `40.1.1.0/24`
- `40.1.2.0/24`
- `40.2.1.0/24`
- `40.2.2.0/24`
- `50.1.1.0/24`
- `50.1.3.0/24`
- `50.2.1.0/24`
- `50.2.3.0/24`
- `100.1.1.0/24`
- `100.2.1.0/24`
- `100.10.1.0/24`

## Controller connectivity

The Phase 5 verification set shows controller sessions UP over MPLS and public Internet as applicable across the vEdges.

## Full-fabric BFD verification

The preserved Phase 5 device verification set shows the expected MPLS/MPLS, MPLS/public-internet, public-internet/MPLS and public-internet/public-internet BFD combinations in **UP** state across the verified fabric.

**Phase 5 full-fabric BFD acceptance: PASS**
