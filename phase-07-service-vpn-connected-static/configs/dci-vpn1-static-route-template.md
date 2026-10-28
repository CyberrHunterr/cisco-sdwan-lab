# DCI VPN 1 Static Route Template Update

The existing VPN 1 Service Feature Template is updated rather than replaced.

Configured IPv4 static routes:

- `192.168.31.0/24 -> 172.16.31.2`
- `192.168.32.0/24 -> 172.16.31.2`
- `192.168.33.0/24 -> 172.16.31.2`

The change is pushed through the existing Device Template.

Expected Config Diff behavior:

- VPN 1 static route lines are added.
- Phase 6 VPN 0, transport interface, OSPF and VPN 512 configuration remains unchanged.
