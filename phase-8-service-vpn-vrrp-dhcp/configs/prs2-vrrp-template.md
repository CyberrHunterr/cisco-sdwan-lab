# PRS2 VRRP Template Configuration

The Paris VPN 1 LAN interface template contains:

- VRRP Group ID: `50`
- Virtual IP: `172.16.51.254`
- Priority: `150`
- Track OMP: `Enabled`

Resulting device configuration:

```text
vrrp 50
 priority 150
 track-omp
 ipv4 172.16.51.254
!
```

Operational result:

- PRS1 priority 200 → primary
- PRS2 priority 150 → backup
