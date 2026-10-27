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

## vEdge-PRS2 OSPF

The edge showed:

- peer address: `50.1.2.2`
- interface: `ge0/0`
- router ID: `2.2.2.4`
- state: **full**

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

## vEdge-PRS2 controller connectivity

Observed MPLS control sessions:

- vSmart1 `55.55.10.3`: **UP**
- vSmart2 `55.55.10.4`: **UP**

Public Internet sessions were also UP to both vSmarts and vManage.

## PRS2 ↔ DCI BFD verification

All four transport combinations were observed UP:

| Source TLOC | Remote TLOC | State |
|---|---|---|
| MPLS | MPLS | UP |
| MPLS | public-internet | UP |
| public-internet | MPLS | UP |
| public-internet | public-internet | UP |

## Full-fabric limitation

The vEdge-DC-DCI capture also contained DOWN BFD sessions toward `55.55.55.40`.

Therefore this phase should not be represented as a complete all-edge BFD success snapshot.
