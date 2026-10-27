# Template Mapping

The Phase 6 Device Template mirrors the existing vEdge-DC-DCI configuration.

## System

Mapped through:

- WG3-System
- WG3-System-AAA
- WG3-System-BFD
- WG3-System-OMP
- WG3-System-Security

Device-specific fields include:

- hostname
- system-ip
- site-id

## VPN 0

Preserved behavior includes:

- default route `0.0.0.0/0 -> 30.2.1.2`
- public-Internet interface `ge0/0`
- MPLS interface `ge0/1`
- tunnel-interface configuration
- transport colors
- allow-service settings
- OSPF router-id `55.55.55.30`
- OSPF area 0
- `ge0/1` as point-to-point OSPF interface

## VPN 512

The management VPN and its interface are represented in the Device Template.

## Acceptance principle

The configuration source changes from CLI to vManage, while network behavior must remain unchanged.
