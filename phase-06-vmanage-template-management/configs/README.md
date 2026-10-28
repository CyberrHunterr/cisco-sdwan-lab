# Phase 6 Template Set

Phase 6 configuration is represented as vManage templates rather than direct CLI configuration.

## Basic Information Feature Templates

- WG3-System
- WG3-System-AAA
- WG3-System-BFD
- WG3-System-OMP
- WG3-System-Security

## Transport and Management Templates

The Device Template also represents:

- VPN 0
- public-Internet transport interface
- MPLS transport interface
- VPN 0 OSPF
- VPN 512
- VPN 512 management interface

## Device Template

- WG3-vEdge-Template

## Device-specific values

For vEdge-DC-DCI:

- Hostname: vEdge-DC-DCI
- System IP: 55.55.55.30
- Site ID: 30
- Public Internet interface IP: 30.2.1.1/24
- MPLS interface IP: 30.1.1.1/24

The template must preserve the existing control-plane and transport behavior.
