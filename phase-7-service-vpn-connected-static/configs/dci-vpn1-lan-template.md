# DCI VPN 1 LAN Interface Template

Target device: `vEdge-DC-DCI`

Feature template role:

- VPN Interface Ethernet
- Service VPN: `1`
- Interface: `ge0/3`
- IPv4 Address: `172.16.31.1/24`
- Shutdown: `No`
- Tunnel Interface: **Off**

The LAN interface is a service-side interface and therefore does not receive an SD-WAN transport color.

The IPv4 address is treated as a Device Specific value in the template workflow.
