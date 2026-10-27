# Phase 5 — MPLS Transport Bring-Up

Phase 5 extends the SD-WAN fabric from Internet-only reachability to dual-transport operation using **MPLS + public Internet**.

The phase has four technical objectives:

1. standardize selected MPLS backbone links as OSPF point-to-point,
2. extend OSPF reachability to the MPLS-facing vEdge interfaces,
3. verify MPLS routing and controller reachability,
4. interconnect the Internet and MPLS transport domains so cross-transport BFD sessions can form.

## Verified result

Phase 5 verification confirms:

- MPLS-facing vEdge OSPF adjacencies: **FULL**
- MPLS/core routes learned through OSPF
- controller connectivity over the available MPLS and public-Internet transports: **UP**
- MPLS-P3 ↔ Internet Router OSPF adjacency over `3.3.3.0/30`: **FULL**
- cross-transport BFD combinations across the verified fabric: **UP**

### BFD transport combinations

- MPLS → MPLS: **UP**
- MPLS → public Internet: **UP**
- public Internet → MPLS: **UP**
- public Internet → public Internet: **UP**

**Phase 5 status: ✅ Complete**

## Evidence

- [verification/device-verification/](verification/device-verification/)
- [verification/observed-transport-state.md](verification/observed-transport-state.md)
- [verification/phase5-checklist.md](verification/phase5-checklist.md)
- [verification/raw/](verification/raw/)

## Configuration set

The complete Phase 5 configuration set is documented under [configs/](configs/):

### Backbone
- PE Router point-to-point OSPF
- MPLS-P1 point-to-point OSPF
- MPLS-P4 point-to-point OSPF
- Internet Router ↔ MPLS-P3 3.3.3.0/30 OSPF interconnect

### vEdges
- vEdge-DRC-Cyber2
- vEdge-DC-DCI
- vEdge-PRS1
- vEdge-PRS2
- vEdge-PRS3
- vEdge-LDN1
- vEdge-LDN2

These are normalized phase-specific snippets supported by the preserved Phase 5 evidence, not fabricated full running-config captures.

The task heading references MPLS-P2, but the supplied guide does not provide a specific MPLS-P2 interface mapping for this change, so no unsupported MPLS-P2 config is invented.
