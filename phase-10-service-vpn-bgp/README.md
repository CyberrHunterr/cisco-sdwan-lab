# Phase 10 — Service VPN: BGP & Localized Route Policy

Phase 10 introduces BGP on **VPN 2** between the London site and Data Center, then applies localized route policy to control preferred paths.

The phase is kept as one repository phase with two sections:

1. **Section 1 — iBGP & eBGP**
2. **Section 2 — Localized Route Policy**

## Scope

### London — Site 40 / AS 65040

- vEdge-LDN1 — CLI-managed
- vEdge-LDN2 — vManage-template-managed
- SITE-LONDON2 — LAN router

### Data Center — Site 30 / AS 65030

- vEdge-DC-DCI — vManage-template-managed
- DC2-DCI — LAN router

### Disaster Recovery — Site 20 / AS 65020

- vEdge-DRC-Cyber2 — eBGP peer used by the localized-policy design

## Section 1 — iBGP & eBGP

The first section builds BGP reachability over VPN 2.

Key design points:

- London iBGP uses AS `65040`
- DC iBGP uses AS `65030`
- London ↔ DC uses eBGP
- BGP peering uses loopback addresses
- OSPF provides loopback reachability
- OSPF administrative distance is raised to 210 so iBGP routes can be preferred
- eBGP loopback peering uses `ebgp-multihop 2`
- `update-source loopback0` is used on loopback-based BGP sessions

### Final routing result

SITE-LONDON2 learns:

- `192.168.36.0/24`
- `192.168.37.0/24`
- `192.168.38.0/24`

through BGP.

DC2-DCI learns:

- `192.168.46.0/24`
- `192.168.47.0/24`
- `192.168.48.0/24`

through BGP.

### End-to-end validation

Final sourced ICMP validation completed successfully in both directions.

SITE-LONDON2:

- `192.168.46.10 → 192.168.36.10`: 5/5 — 100%
- `192.168.46.10 → 192.168.37.10`: 5/5 — 100%
- `192.168.46.10 → 192.168.38.10`: 5/5 — 100%

DC2-DCI:

- `192.168.36.10 → 192.168.46.10`: 5/5 — 100%
- `192.168.36.10 → 192.168.47.10`: 5/5 — 100%
- `192.168.36.10 → 192.168.48.10`: 5/5 — 100%

## Section 2 — Localized Route Policy

Section 2 applies per-device BGP route policy on the London vEdges.

The design uses two BGP attributes:

- **Local Preference** to control London outbound path selection
- **AS-Path Prepend** to influence remote-site return-path selection

### vEdge-LDN1

LDN1 applies:

- Local Preference 1000 to DRC prefixes
- normal preference to DC prefixes
- AS-path prepend toward DC for London LAN prefixes

### vEdge-LDN2

LDN2 applies:

- Local Preference 1000 to DC prefixes
- normal preference to DRC prefixes
- AS-path prepend toward Cyber2 for London LAN prefixes

### Verified DC path selection

SITE-LONDON2 shows the DC prefixes through both London vEdges and selects the LDN2 path with **Local Preference 1000**.

For `192.168.36/37/38.0/24`:

- path through `40.40.40.1`: Local Preference 100
- path through `40.40.40.2`: Local Preference 1000 — selected

A traceroute from SITE-LONDON2 to DC begins with:

- first hop `172.16.42.3` — vEdge-LDN2

This confirms the intended London → DC path.

### Verified DC return-path selection

On vEdge-DC-DCI, London LAN prefixes have two external BGP paths.

For `192.168.46/47/48.0/24`:

- via LDN1: AS path `65040 11111`
- via LDN2: AS path `65040` — selected best path

This confirms the AS-path prepend applied by LDN1 makes LDN2 the preferred DC → London path.

### Verified Cyber2 return-path selection

On vEdge-DRC-Cyber2, London LAN prefixes also have two BGP paths.

For `192.168.46/47/48.0/24`:

- via LDN1: AS path `65040` — selected best path
- via LDN2: AS path `65040 65040`

This confirms the LDN2 prepend makes LDN1 the preferred Cyber2 → London path.

## Troubleshooting and corrections

During implementation, several configuration issues were corrected:

- SITE-LONDON2 LAN interface IP/addressing was completed and the interface was enabled.
- London and DC LAN-facing OSPF interfaces were corrected from point-to-point behavior to broadcast/default Ethernet behavior, after which OSPF neighbors reached FULL state.
- missing `update-source loopback0` statements were added to loopback-based BGP neighbors.
- `next-hop-self` was added on the DC-DCI LAN-side iBGP relationship so downstream BGP routes used a reachable next hop.

After these corrections:

- OSPF adjacencies reached FULL
- BGP sessions reached ESTABLISHED
- expected remote prefixes were learned through BGP
- bidirectional end-to-end ping validation passed at 100%

## Evidence

- [verification/cli-evidence/](verification/cli-evidence/)
- [verification/images/](verification/images/)
- [verification/phase10-checklist.md](verification/phase10-checklist.md)
- [docs/troubleshooting.md](docs/troubleshooting.md)

## Phase status

**✅ Phase 10 complete — VPN 2 iBGP/eBGP routing, localized route policy, preferred-path selection and bidirectional reachability verified.**
