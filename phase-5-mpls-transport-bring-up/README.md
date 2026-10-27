# Phase 5 — MPLS Transport Bring-Up

Phase 5 extends the SD-WAN fabric from Internet-only reachability to dual-transport operation using **MPLS + public Internet**.

The phase has four technical objectives:

1. standardize selected MPLS backbone links as OSPF point-to-point,
2. extend OSPF reachability to the MPLS-facing vEdge interfaces,
3. verify MPLS routing and controller reachability,
4. interconnect the Internet and MPLS transport domains so cross-transport BFD sessions can form.

## Verified path

The strongest live verification path captured for this phase is:

**vEdge-PRS2 (55.55.55.51) ↔ vEdge-DC-DCI (55.55.55.30)**

Observed results:

- vEdge-PRS2 OSPF neighbor on the MPLS-facing interface: **FULL**
- MPLS routes learned over `ge0/0`
- vSmart1 and vSmart2 control connections over MPLS: **UP**
- vEdge-PRS2 ↔ vEdge-DC-DCI BFD:
  - MPLS → MPLS: **UP**
  - MPLS → public Internet: **UP**
  - public Internet → MPLS: **UP**
  - public Internet → public Internet: **UP**
- MPLS-P3 ↔ Internet Router OSPF adjacency over `3.3.3.0/30`: **FULL**

## Important scope note

This is **not** a claim that every BFD session in the full lab was UP at the time of capture.

The live vEdge-DC-DCI output still showed DOWN sessions toward system IP `55.55.55.40`. Those lines are preserved in raw evidence.

Accordingly, Phase 5 is documented as:

> Core transport bring-up verified, cross-transport BFD verified on the PRS2↔DCI path, full-fabric BFD verification partial.

## Evidence

- [verification/observed-transport-state.md](verification/observed-transport-state.md)
- [verification/phase5-checklist.md](verification/phase5-checklist.md)
- [verification/raw/](verification/raw/)

## Configuration notes

The phase-specific examples are documented under [configs/](configs/). These are normalized configuration snippets based on the lab workflow, not fabricated full running-config captures.
