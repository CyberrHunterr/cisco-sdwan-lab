# VPN 0 Transport Template

The VPN 0 template reproduces the existing transport VPN configuration of vEdge-DC-DCI.

## VPN

- VPN ID: `0`

## Default route

- Prefix: `0.0.0.0/0`
- Next hop: `30.2.1.2`

## Public Internet interface

- Interface: `ge0/0`
- IPv4 address: `30.2.1.1/24`
- Shutdown: `No`
- Tunnel Interface: `On`
- Encapsulation: `ipsec`
- Color: `public-internet`

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
