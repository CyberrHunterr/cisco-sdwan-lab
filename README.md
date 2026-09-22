# Cisco SD-WAN Lab

A multi-phase Cisco SD-WAN lab project documented as a reproducible engineering portfolio.

The repository is organized by phase. Each phase separates:

- architecture and intent,
- device configuration,
- verification evidence,
- reconstruction notes and scope boundaries.

> **Project context:** This was completed as a collaborative WG3 lab project. The repository documents the complete technical implementation rather than only one participant's assigned task.

## Project Roadmap

| Phase | Scope | Repository Status |
|---|---|---|
| Phase 1 | Underlay, OSPF, MPLS/LDP, Internet reachability | ✅ Initial public version |
| Phase 2 | vBond, vSmart, vManage controller deployment | Planned |
| Phase 3 | PKI, Root CA, controller onboarding | Planned |
| Later phases | Edge onboarding and additional SD-WAN functions | Planned |

## Phase 1

Open [`phase-1-underlay/`](phase-1-underlay/) for the first completed project package.

### Phase 1 covers

- underlay design,
- PE Router configuration,
- MPLS core routers P1–P4,
- OSPF Area 0,
- MPLS/LDP,
- Internet Router default routing,
- adjacency and forwarding verification.

## Evidence Policy

The lab is currently at a later phase, so the live running configuration contains changes introduced after Phase 1.

For that reason, the Phase 1 configuration files in this repository are **reconstructed Phase 1 configurations**, not raw present-day `show running-config` dumps.

The reconstruction uses:

1. original Phase 1 task scope,
2. historical Phase 1 configuration/verification notes,
3. later live device captures only where they confirm Phase 1-relevant infrastructure.

Later-phase configuration is intentionally excluded.

See [`phase-1-underlay/docs/reconstruction-notes.md`](phase-1-underlay/docs/reconstruction-notes.md).

## Topology

Full lab topology is available at [`phase-1-underlay/topology/full-lab-topology.png`](phase-1-underlay/topology/full-lab-topology.png).
