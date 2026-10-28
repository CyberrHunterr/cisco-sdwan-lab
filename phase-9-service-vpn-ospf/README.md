# Phase 9 — Service VPN: OSPF

Phase 9 replaces the Paris branch's manually maintained LAN reachability with dynamic OSPF routing inside **VPN 1**.

The phase proves both directions of the service-routing chain:

- **LAN → Overlay:** SITE-PARIS1 advertises its LAN networks to the Paris vEdges through OSPF; the vEdges then carry those networks into the SD-WAN fabric through OMP.
- **Overlay → LAN:** remote OMP routes are redistributed into OSPF so SITE-PARIS1 can reach remote service networks.
- **Default routing:** the Paris vEdges originate a default route toward the LAN router.

## Scope

Site: **Branch Paris — Site ID 50**

Devices:

- **SITE-PARIS1** — LAN router, CLI-managed
- **vEdge-PRS1** — VPN 1 OSPF configured through CLI
- **vEdge-PRS2** — VPN 1 OSPF configured through vManage templates
- **vEdge-DRC-Cyber2** and **vEdge-DC-DCI** — remote verification devices; their Phase 9 SD-WAN configuration is not changed

Out of scope:

- vEdge-PRS3 / VPN 2
- London / BGP work assigned to the next phase

## Paris OSPF design

| Item | Value |
|---|---|
| Paris VPN 1 segment | `172.16.51.0/24` |
| SITE-PARIS1 segment IP observed | `172.16.51.69` |
| SITE-PARIS1 OSPF router-id | `50.50.50.100` |
| PRS1 router-id | `55.55.55.50` |
| PRS2 router-id | `55.55.55.51` |
| OSPF area | Area 0 |
| Network type | Broadcast |
| PRS1 ge0/2 cost | 5 |
| PRS2 ge0/2 cost | 6 |
| Paris LAN prefixes | `192.168.51.0/24`, `192.168.52.0/24`, `192.168.53.0/24` |
| Overlay → LAN | `redistribute omp` |
| Default route toward LAN | `default-information originate` |

## Configuration model

### SITE-PARIS1

SITE-PARIS1 provides the LAN-facing OSPF endpoint and advertises three /24 loopback networks:

- `192.168.51.0/24`
- `192.168.52.0/24`
- `192.168.53.0/24`

The loopbacks use OSPF point-to-point network type so the /24 prefixes are advertised instead of /32 host routes.

See:

- [configs/site-paris1-ospf.cfg](configs/site-paris1-ospf.cfg)

### vEdge-PRS1 — CLI

PRS1 runs VPN 1 OSPF with:

- router-id `55.55.55.50`
- `default-information originate`
- `redistribute omp`
- area 0
- `ge0/2` cost 5

The older Paris LAN static routes are removed only after OSPF adjacency and route learning are confirmed.

See:

- [configs/vedge-prs1-vpn1-ospf.cfg](configs/vedge-prs1-vpn1-ospf.cfg)

### vEdge-PRS2 — vManage Template

PRS2 uses the same routing intent through vManage:

- router-id `55.55.55.51`
- OMP redistribution
- area 0
- `ge0/2`
- cost 6
- default-route origination

The template push is validated through Config Diff and Push Success evidence.

See:

- [configs/vedge-prs2-template.md](configs/vedge-prs2-template.md)

## Verified OSPF adjacencies

The preserved CLI evidence shows:

- PRS1 sees PRS2 and SITE-PARIS1 as FULL neighbors.
- PRS2 sees PRS1 and SITE-PARIS1 as FULL neighbors.
- SITE-PARIS1 sees:
  - PRS1 `55.55.55.50` as **FULL/BDR**
  - PRS2 `55.55.55.51` as **FULL/DROTHER**

This confirms the expected broadcast-segment DR/BDR behavior.

## Dynamic route transition

After the previous static routes are removed, both Paris vEdges learn:

- `192.168.51.0/24`
- `192.168.52.0/24`
- `192.168.53.0/24`

through **OSPF IA**, using SITE-PARIS1 as the LAN-side next hop.

This is the core Phase 9 transition from manually maintained static routes to dynamic service-side routing.

## Overlay → LAN verification

SITE-PARIS1 learns remote service networks through OSPF after the Paris vEdges redistribute OMP routes into OSPF.

The preserved report evidence includes remote Cyber2, DCI and other service prefixes in the SITE-PARIS1 route table, plus a default route toward the Paris gateway.

## Return-path correction and successful end-to-end test

During end-to-end validation, the Cyber2 LAN router required explicit return routes toward the Paris LAN networks.

The following routes were added on **DRC1-CYBER2**:

```text
ip route 192.168.51.0 255.255.255.0 172.16.21.1
ip route 192.168.52.0 255.255.255.0 172.16.21.1
ip route 192.168.53.0 255.255.255.0 172.16.21.1
```

After the return path was present, sourced pings from Paris succeeded:

- `192.168.51.1 → 192.168.21.1`: **5/5**
- `192.168.51.1 → 192.168.22.1`: **5/5**
- `192.168.51.1 → 192.168.23.1`: **5/5**

See:

- [verification/report-transcriptions/drc1-cyber2-paris-return-routes.txt](verification/report-transcriptions/drc1-cyber2-paris-return-routes.txt)
- [verification/report-transcriptions/site-paris1-cyber2-end-to-end-ping.txt](verification/report-transcriptions/site-paris1-cyber2-end-to-end-ping.txt)

## Phase 8 continuity

The OSPF work did not replace the Phase 8 gateway services.

Preserved verification shows:

- PRS1 remains VRRP **primary**, priority 200
- PRS2 remains VRRP **backup**, priority 150
- OMP remains UP
- DHCP configuration remains present

See:

- [verification/report-transcriptions/phase8-continuity-checks.txt](verification/report-transcriptions/phase8-continuity-checks.txt)

## Screenshot evidence

The selected screenshot set for this phase is stored under:

- [verification/images/](verification/images/)

The evidence set is intentionally selective rather than duplicating every screenshot from the working report. It covers:

- SITE-PARIS1 interface and OSPF state
- PRS1 OSPF interface, neighbors and final routes
- PRS2 template Config Diff and Push Success
- PRS2 running configuration, neighbors and final routes
- SITE-PARIS1 DR/BDR view
- PRS1/PRS2 VRRP continuity
- Cyber2 return-route correction
- successful Paris → Cyber2 sourced ping validation

## Text evidence

Terminal screenshots from the working report were transcribed only where values were clearly readable.

These transcriptions are **not raw terminal captures** and are labeled accordingly:

- [verification/report-transcriptions/](verification/report-transcriptions/)

## Acceptance

See:

- [verification/phase9-checklist.md](verification/phase9-checklist.md)
- [docs/evidence-notes.md](docs/evidence-notes.md)

## Phase status

**✅ Phase 9 complete — Paris VPN 1 OSPF adjacency, dynamic LAN route learning, OMP-to-OSPF redistribution, template deployment, return-path correction and successful end-to-end reachability verified.**
