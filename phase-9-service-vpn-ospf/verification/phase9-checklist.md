# Phase 9 Verification Checklist

## SITE-PARIS1

- [x] Paris LAN interface is UP in `172.16.51.0/24`
- [x] observed segment address: `172.16.51.69`
- [x] OSPF process 1 present
- [x] router-id `50.50.50.100`
- [x] Area 0 used
- [x] LAN interface participates in OSPF
- [x] both Paris vEdges visible as OSPF neighbors
- [x] PRS1 observed as FULL/BDR
- [x] PRS2 observed as FULL/DROTHER
- [x] remote service networks learned through OSPF
- [x] default route present toward Paris gateway

## vEdge-PRS1 — CLI

- [x] VPN 1 OSPF configured
- [x] router-id `55.55.55.50`
- [x] `default-information originate`
- [x] `redistribute omp`
- [x] Area 0 / `ge0/2`
- [x] OSPF cost 5
- [x] SITE-PARIS1 adjacency FULL
- [x] PRS2 adjacency FULL
- [x] Paris LAN prefixes learned through OSPF
- [x] `192.168.51.0/24` = OSPF IA
- [x] `192.168.52.0/24` = OSPF IA
- [x] `192.168.53.0/24` = OSPF IA
- [x] previous Paris static routes removed after OSPF verification
- [x] VRRP remains primary / priority 200
- [x] DHCP configuration remains present

## vEdge-PRS2 — Template

- [x] VPN 1 OSPF Feature Template added
- [x] router-id `55.55.55.51`
- [x] OMP redistribution configured
- [x] default-route origination configured
- [x] Area 0 / `ge0/2`
- [x] OSPF cost 6
- [x] Config Diff evidence preserved
- [x] Push Success evidence preserved
- [x] running configuration confirms OSPF block
- [x] PRS1 adjacency FULL
- [x] SITE-PARIS1 adjacency FULL
- [x] Paris LAN prefixes learned through OSPF IA
- [x] VRRP remains backup / priority 150
- [x] OMP remains UP
- [x] DHCP configuration remains present

## LAN → Overlay

- [x] Paris LAN prefixes learned by PRS1 through OSPF
- [x] Paris LAN prefixes learned by PRS2 through OSPF
- [x] OSPF-learned Paris networks are carried into the SD-WAN service-routing domain

## Overlay → LAN

- [x] remote service prefixes visible on SITE-PARIS1
- [x] OMP-to-OSPF redistribution verified by route-table evidence
- [x] default route visible on SITE-PARIS1

## End-to-end / return path

- [x] missing Cyber2-side return path identified
- [x] return routes for `192.168.51/52/53.0/24` added through `172.16.21.1`
- [x] Paris source `192.168.51.1` → `192.168.21.1`: 5/5
- [x] Paris source `192.168.51.1` → `192.168.22.1`: 5/5
- [x] Paris source `192.168.51.1` → `192.168.23.1`: 5/5

## Evidence quality

- [x] CLI verification evidence preserved
- [x] selected screenshot evidence preserved
- [x] failed/superseded end-to-end screenshot removed from acceptance evidence
- [x] Phase 8 state distinguished from Phase 9 acceptance criteria

## Result

**PASS — Phase 9 acceptance criteria are satisfied by the preserved routing, adjacency, template and end-to-end evidence.**
