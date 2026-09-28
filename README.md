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
| Phase 1 | Underlay, OSPF, MPLS/LDP, Internet reachability | ✅ Complete |
| Phase 2 | vBond, vSmart, vManage controller deployment | ✅ Complete |
| Phase 3 | PKI, Root CA, controller onboarding | ✅ Complete |
| Phase 4 | vEdge certificate installation and onboarding | Planned |
| Later phases | Transport and additional SD-WAN functions | Planned |

## Phase 1 — Underlay Infrastructure

Open [phase-1-underlay/](phase-1-underlay/) for:

- underlay design,
- PE Router configuration,
- MPLS core routers P1–P4,
- OSPF Area 0,
- MPLS/LDP,
- Internet Router default routing,
- adjacency and forwarding verification.

## Phase 2 — Controller Deployment

Open [phase-2-controllers/](phase-2-controllers/) for:

- vBond deployment,
- vSmart1 and vSmart2 deployment,
- vManage deployment,
- VPN 0 / VPN 512 addressing,
- controller reachability,
- vManage GUI and controller inventory validation.

## Phase 3 — PKI and Controller Onboarding

Open [phase-3-pki-controller-onboarding/](phase-3-pki-controller-onboarding/) for:

- IOS Root CA configuration,
- enterprise root certificate distribution,
- vManage identity certificate onboarding,
- vBond identity certificate onboarding,
- vSmart1 and vSmart2 identity certificate onboarding,
- controller certificate-state validation,
- DTLS controller-to-controller verification.

## Evidence Policy

The lab has progressed beyond the earlier phases, so current device state can contain configuration and sessions introduced later in the project.

Each phase therefore separates:

1. phase-specific configuration and workflow,
2. summarized/normalized verification,
3. preserved raw CLI evidence under `verification/raw/` where available,
4. later-phase state that must be excluded from that phase's acceptance criteria.

Raw evidence is never invented. If an original terminal capture was not preserved as text, the repository keeps the available historical report or exact preserved excerpt instead of recreating a fake CLI output.

Secrets, password hashes, private keys and other sensitive authentication material are intentionally excluded from the public repository.

## Topology

Full lab topology is available at [phase-1-underlay/topology/full-lab-topology.png](phase-1-underlay/topology/full-lab-topology.png).
