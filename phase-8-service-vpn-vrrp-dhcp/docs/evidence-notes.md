# Evidence Notes

Phase 8 acceptance is based on current device output plus the preserved project report.

## Verified directly from current CLI

PRS1:

- VPN 1 LAN IP 172.16.51.1/24
- VRRP group 50
- priority 200
- state primary
- OMP state up
- DHCP server configuration
- DHCP default gateway 172.16.51.254

PRS2:

- VPN 1 LAN IP 172.16.51.2/24
- VRRP group 50
- priority 150
- state backup
- OMP state up
- DHCP server configuration
- DHCP binding 172.16.51.69
- controller connections up
- BFD sessions up

## Later-phase state

The current running configuration contains VPN 1 OSPF state from later work. It is intentionally excluded from Phase 8 acceptance.

## Failover

The project report documents the intended and performed failover workflow. A separate preserved terminal capture of the live failover state has not yet been added to this repository, so failover remains explicitly marked as pending evidence rather than reconstructed.
