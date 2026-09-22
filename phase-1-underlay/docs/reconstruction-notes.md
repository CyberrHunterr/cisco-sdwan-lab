# Reconstruction Notes

## Why Reconstruction Was Necessary

The lab has progressed well beyond Phase 1. The present-day device configuration therefore contains settings introduced during later phases.

Publishing the current `show running-config` output as "Phase 1" would be misleading.

For that reason, this repository reconstructs the Phase 1 state.

## Evidence Priority

The reconstruction uses the following priority:

1. **Historical Phase 1 implementation evidence**
2. **Original Phase 1 task scope**
3. **Current live state, only when it confirms Phase 1-relevant infrastructure**

## High-Confidence Phase 1 Items

### Internet Router

Historical Phase 1 evidence confirms:

- external interface used for default routing,
- default route:
  `ip route 0.0.0.0 0.0.0.0 Ethernet2/0`,
- successful ICMP test to PE-ROUTER `100.2.1.1`.

### PE-ROUTER

Historical Phase 1 evidence confirms:

- `100.1.1.1` link toward MPLS-P1,
- `100.2.1.1` link toward Internet Router,
- OSPF process 1,
- OSPF router ID `1.1.1.0`,
- Phase 1 OSPF networks `100.1.1.0/24` and `100.2.1.0/24`,
- MPLS enabled,
- LDP selected as label protocol,
- MPLS enabled on Ethernet0/2 and Ethernet0/3,
- default route via `100.2.1.2`,
- successful OSPF/MPLS/LDP verification.

### MPLS Core

The original task scope defines P1–P4 as the MPLS/OSPF/LDP backbone.

Current captures confirm the core links and adjacencies:

- PE ↔ P1: `100.1.1.0/24`
- P1 ↔ P2: `5.5.5.0/30`
- P1 ↔ P3: `6.6.6.0/30`
- P2 ↔ P4: `7.7.7.0/30`
- P3 ↔ P4: `8.8.8.0/30`

## Intentionally Excluded

The following present-day configuration is not included in the Phase 1 reconstructed core unless Phase 1-period evidence is found later:

- P1 site-facing `20.1.1.0/24` and `30.1.1.0/24`,
- P4 site-facing `40.1.x.0/24` and `50.1.x.0/24` links,
- P3 ↔ Internet Router `3.3.3.0/30` path,
- later `172.16.x.0/24` static routes,
- present-day NAT configuration,
- later controller/edge-related routes and adjacencies,
- current non-core OSPF neighbors.

These items may eventually belong to Phase 1 if additional historical evidence proves they were introduced then. Until that evidence exists, the public project uses the conservative reconstruction.

## Configuration Files Are Not Raw Snapshots

Every file under `configs/` should be read as:

> a reconstructed Phase 1 configuration derived from available project evidence.

It should not be represented as a literal archived running-config captured on the exact day Phase 1 ended.
