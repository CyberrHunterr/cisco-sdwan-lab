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
| Phase 4 | vEdge certificate installation and onboarding | ✅ Complete |
| Phase 5 | MPLS transport bring-up, OSPF and BFD verification | ✅ Complete |
| Phase 6 | vManage Feature/Device Template management | ✅ Complete |
| Phase 7 | Service VPN 1, connected/static routes, OMP propagation | ✅ Complete |
| Later phases | Additional SD-WAN service functions | Planned |

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

## Phase 4 — vEdge Certificate Installation and Onboarding

Open [phase-4-vedge-onboarding/](phase-4-vedge-onboarding/) for:

- vEdge system and transport baseline,
- Root CA installation,
- CSR / identity-certificate workflow,
- chassis and serial registration,
- live controller-connection verification,
- OMP peer verification,
- preserved raw vEdge and vSmart CLI evidence.

## Phase 5 — MPLS Transport Bring-Up

Open [phase-5-mpls-transport-bring-up/](phase-5-mpls-transport-bring-up/) for:

- MPLS-side OSPF extension,
- Internet Router ↔ MPLS-P3 interconnect,
- vEdge transport-side routing,
- full-fabric BFD verification.

## Phase 6 — vManage Template Management

Open [phase-6-vmanage-template-management/](phase-6-vmanage-template-management/) for:

- System/AAA/BFD/OMP/Security Feature Templates,
- VPN 0, MPLS, Internet, OSPF and VPN 512 templates,
- Device Template assembly,
- Device Specific values,
- template push and post-push CLI verification.

## Phase 7 — Service VPN Connected & Static Routes

Open [phase-7-service-vpn-connected-static/](phase-7-service-vpn-connected-static/) for:

- VPN 1 connected routing,
- VPN 1 static routing,
- CLI-managed Cyber2 configuration,
- vManage-template-managed DCI configuration,
- OMP propagation,
- VPN-aware ping/traceroute verification,
- CLI vs Template comparison.

GUI screenshots for the Phase 7 template workflow may be added later as supplemental evidence; the preserved CLI and routing evidence already validates the operational result.

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
