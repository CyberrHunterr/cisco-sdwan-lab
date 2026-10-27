# VPN 0 MPLS Interface Template

This template reproduces the MPLS-facing transport interface of vEdge-DC-DCI.

- Interface: `ge0/1`
- IPv4 address: `30.1.1.1/24`
- Shutdown: `No`
- Tunnel Interface: `On`
- Encapsulation: `ipsec`
- Color: `mpls`

Observed service state retained from the device:

- allow-service all
- no allow-service bgp
- allow-service dhcp
- allow-service dns
- allow-service icmp
- no allow-service sshd
- no allow-service netconf
- no allow-service ntp
- no allow-service ospf
- no allow-service stun
- allow-service https

The interface IP is treated as **Device Specific**.
