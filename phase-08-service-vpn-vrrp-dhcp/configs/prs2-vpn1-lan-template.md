# PRS2 VPN 1 LAN Interface Template

Target device: `vEdge-PRS2`

Configured values:

- VPN: `1`
- interface: `ge0/2`
- IPv4 address: `172.16.51.2/24`
- shutdown: `No`
- service-side interface
- tunnel interface: `Off`

Resulting device configuration:

```text
vpn 1
 interface ge0/2
  ip address 172.16.51.2/24
  no shutdown
 !
!
```
