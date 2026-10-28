# Phase 11 — vSmart Template & Centralized Policy (Hub & Spoke)

Phase 11 is the final phase of the WG3 SD-WAN lab program.

This phase moves control-plane behavior from per-device configuration to a centralized policy model. The target topology is:

- **Hub:** Head Office — Site 1 — vEdge-HO
- **Spokes:** DRC — Site 20 — vEdge-DRC-Cyber2
- **Spokes:** Paris — Site 50 — vEdge-PRS1 / PRS2 / PRS3
- **Out of scope:** London — Site 40
- **Out of scope:** Data Center — Site 30
- **Policy scope:** VPN 1

## What changed

Before the policy, the SD-WAN overlay behaved as a full mesh.

After the centralized control policy:

- Paris and DRC are treated as spokes.
- Head Office is the hub.
- Spoke-to-spoke traffic is steered through Head Office.
- London and Data Center remain outside the policy scope.

## Centralized policy

The final control policy contains:

- Site list `HO-HUB` → Site 1
- Site list `PRS-DRC-SPOKE` → Sites 20 and 50
- VPN list `VPN1` → VPN 1
- TLOC list `HUB-HO-TLOC` → system IP `55.55.55.1`, color `mpls`, encap `ipsec`
- Control policy `HS-PRS-DRC`
- `default-action reject`

The same centralized policy is present on both vSmart1 and vSmart2.

## Hub route correction

Hub-and-spoke policy alone causes the spokes to stop learning each other's specific routes directly.

The final Head Office correction is:

```text
vpn 1
 ip route 0.0.0.0/0 null0
 omp
  advertise static
 !
!
```

This gives the spokes a default route toward the hub and allows spoke-to-spoke traffic to transit Head Office without creating a routing loop.

## Final verification

### vSmart

- vSmart1 centralized policy present
- vSmart1 apply-policy present
- vSmart2 centralized policy present
- vSmart2 apply-policy present
- control connections remain UP

### Hub

- `0.0.0.0/0` installed as a static Null0 route
- static route advertised through OMP

### Paris spoke

- default route learned through OMP
- hub TLOC: `55.55.55.1`

### DRC spoke

- default route learned through OMP
- hub TLOC: `55.55.55.1`

### Path validation

Paris → DRC:

```text
SITE-PARIS1# traceroute 172.16.21.1

1  172.16.51.254
2  172.16.1.1
3  172.16.21.1
```

DRC → Paris:

```text
DRC1-CYBER2# traceroute 172.16.51.1

1  172.16.21.1
2  172.16.1.1
3  172.16.51.1
```

The path evidence shows that spoke-to-spoke traffic is no longer direct and traverses the Head Office hub.

## Configuration files

Final Phase 11 configuration references are stored under [configs/](configs/):

- [vsmart1-centralized-policy.conf](configs/vsmart1-centralized-policy.conf)
- [vsmart2-centralized-policy.conf](configs/vsmart2-centralized-policy.conf)
- [vedge-ho-vpn1.conf](configs/vedge-ho-vpn1.conf)

## Repository evidence

- [verification/cli-evidence/](verification/cli-evidence/)
- [verification/images/](verification/images/)
- [verification/phase11-checklist.md](verification/phase11-checklist.md)
- [docs/troubleshooting.md](docs/troubleshooting.md)

## Phase status

**✅ Phase 11 complete — centralized Hub & Spoke policy and hub-transit forwarding verified.**

This completes the 11-phase WG3 Cisco SD-WAN lab program.
