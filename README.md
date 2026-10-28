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
| Phase 8 | Paris branch VRRP, DHCP and failover | ✅ Complete |
| Phase 9 | Paris Service VPN OSPF, LAN↔overlay route exchange | ✅ Complete |
| Phase 10 | VPN 2 BGP, iBGP/eBGP and localized route policy | ✅ Complete |
| Phase 11 | vSmart templates, centralized policy, Hub & Spoke | ✅ Complete |
| Program | WG3 Cisco SD-WAN lab | ✅ 11 / 11 Complete |

## Phase 1 — Underlay Infrastructure

Open [phase-01-underlay/](phase-01-underlay/) for:

- underlay design,
- PE Router configuration,
- MPLS core routers P1–P4,
- OSPF Area 0,
- MPLS/LDP,
- Internet Router default routing,
- adjacency and forwarding verification.

## Phase 2 — Controller Deployment

Open [phase-02-controllers/](phase-02-controllers/) for:

- vBond deployment,
- vSmart1 and vSmart2 deployment,
- vManage deployment,
- VPN 0 / VPN 512 addressing,
- controller reachability,
- vManage GUI and controller inventory validation.

## Phase 3 — PKI and Controller Onboarding

Open [phase-03-pki-controller-onboarding/](phase-03-pki-controller-onboarding/) for:

- IOS Root CA configuration,
- enterprise root certificate distribution,
- vManage identity certificate onboarding,
- vBond identity certificate onboarding,
- vSmart1 and vSmart2 identity certificate onboarding,
- controller certificate-state validation,
- DTLS controller-to-controller verification.

## Phase 4 — vEdge Certificate Installation and Onboarding

Open [phase-04-vedge-onboarding/](phase-04-vedge-onboarding/) for:

- vEdge system and transport baseline,
- Root CA installation,
- CSR / identity-certificate workflow,
- chassis and serial registration,
- live controller-connection verification,
- OMP peer verification,
- preserved vEdge and vSmart CLI evidence.

## Phase 5 — MPLS Transport Bring-Up

Open [phase-05-mpls-transport-bring-up/](phase-05-mpls-transport-bring-up/) for:

- MPLS-side OSPF extension,
- Internet Router ↔ MPLS-P3 interconnect,
- vEdge transport-side routing,
- full-fabric BFD verification.

## Phase 6 — vManage Template Management

Open [phase-06-vmanage-template-management/](phase-06-vmanage-template-management/) for:

- System/AAA/BFD/OMP/Security Feature Templates,
- VPN 0, MPLS, Internet, OSPF and VPN 512 templates,
- Device Template assembly,
- Device Specific values,
- template push and post-push CLI verification.

## Phase 7 — Service VPN Connected & Static Routes

Open [phase-07-service-vpn-connected-static/](phase-07-service-vpn-connected-static/) for:

- VPN 1 connected routing,
- VPN 1 static routing,
- CLI-managed Cyber2 configuration,
- vManage-template-managed DCI configuration,
- Feature Template and Device Template evidence,
- Config Diff and push-success verification,
- OMP propagation,
- VPN-aware ping/traceroute verification,
- post-push CLI and route-table evidence,
- CLI vs Template comparison.

## Phase 8 — Service VPN: VRRP & DHCP

Open [phase-08-service-vpn-vrrp-dhcp/](phase-08-service-vpn-vrrp-dhcp/) for:

- Paris branch VPN 1 gateway redundancy,
- PRS1 CLI-based VRRP and DHCP,
- PRS2 vManage-template-based VRRP and DHCP,
- Device Template / Feature Template evidence,
- DHCP lease verification,
- VRRP failover and restoration validation,
- preserved vManage screenshots and CLI evidence.

## Phase 9 — Service VPN: OSPF

Open [phase-09-service-vpn-ospf/](phase-09-service-vpn-ospf/) for:

- SITE-PARIS1 LAN-facing OSPF,
- PRS1 CLI-based VPN 1 OSPF,
- PRS2 vManage-template-based VPN 1 OSPF,
- broadcast-segment DR/BDR verification,
- transition from static Paris LAN routes to OSPF,
- OMP → OSPF redistribution,
- default-route origination toward the LAN,
- Phase 8 VRRP/DHCP continuity checks,
- Cyber2 return-path correction,
- successful Paris → Cyber2 sourced ping verification,
- selected image and CLI evidence.

## Phase 10 — Service VPN: BGP & Localized Route Policy

Open [phase-10-service-vpn-bgp/](phase-10-service-vpn-bgp/) for:

- VPN 2 iBGP inside London and Data Center,
- eBGP between London, DC and DRC,
- loopback-based BGP peering,
- OSPF reachability and administrative-distance tuning,
- Local Preference path control,
- AS-Path prepend,
- localized policy on LDN1 and LDN2,
- verified DC and Cyber2 return-path selection,
- bidirectional 100% sourced ping validation,
- implementation troubleshooting and final-state evidence.

## Phase 11 — vSmart Template & Centralized Policy (Hub & Spoke)

Open [phase-11-centralized-policy-hub-spoke/](phase-11-centralized-policy-hub-spoke/) for:

- vSmart centralized-policy state,
- Hub & Spoke control policy,
- Head Office hub definition,
- Paris and DRC spoke definitions,
- VPN 1 policy scope,
- centralized policy on both vSmart controllers,
- Head Office Null0 default route and OMP advertisement,
- spoke default-route verification,
- Paris ↔ DRC hub-transit traceroute evidence,
- final Phase 11 verification checklist.

**WG3 program status: 11 / 11 phases complete.**

## Evidence Policy

The lab has progressed beyond the earlier phases, so current device state can contain configuration and sessions introduced later in the project.

Each phase therefore separates:

1. phase-specific configuration and workflow,
2. summarized/normalized verification,
3. preserved CLI evidence under `verification/cli-evidence/`,
4. later-phase state that must be excluded from that phase's acceptance criteria.

CLI evidence is never fabricated. If an original terminal capture was not preserved as text, the repository keeps the available historical report or exact preserved excerpt instead of recreating a fake CLI output.

Secrets, password hashes, private keys and other sensitive authentication material are intentionally excluded from the public repository.

## Topology

Full lab topology is available at [phase-01-underlay/topology/full-lab-topology.png](phase-01-underlay/topology/full-lab-topology.png).
