# Device Template Assembly

Device Template:

- `WG3-vEdge-Template`

Target device:

- `vEdge-DC-DCI`

## Basic Information

The Device Template includes:

- WG3-System
- WG3-System-AAA
- WG3-System-BFD
- WG3-System-OMP
- WG3-System-Security

## Transport & Management VPN

The Device Template includes:

- VPN 0 transport template
- public-Internet interface template for `ge0/0`
- MPLS interface template for `ge0/1`
- VPN 0 OSPF feature template
- VPN 512 template
- VPN 512 management interface template

## Device Specific values used at attachment

- Hostname: `vEdge-DC-DCI`
- System IP: `55.55.55.30`
- Site ID: `30`
- Public Internet IP: `30.2.1.1/24`
- MPLS IP: `30.1.1.1/24`
- OSPF router ID: `55.55.55.30`

## Push result

The resulting configuration was pushed successfully and the device reported:

- `vManaged: true`
- `Configuration template: WG3-vEdge-Template`
- `Commit pending: false`
