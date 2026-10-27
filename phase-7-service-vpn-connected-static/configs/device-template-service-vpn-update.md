# Device Template Service VPN Update

Existing Device Template:

- `WG3-vEdge-Template`

Target:

- `vEdge-DC-DCI`

Phase 7 extends the existing template by populating the previously empty **Service VPN** section.

## Added components

- VPN 1 Service Feature Template
- VPN 1 LAN Interface Feature Template

## Device Specific value

- VPN 1 LAN IP: `172.16.31.1/24`

## Final generated VPN 1 state

```text
vpn 1
 interface ge0/3
  ip address 172.16.31.1/24
  no shutdown
 !
 ip route 192.168.31.0/24 172.16.31.2
 ip route 192.168.32.0/24 172.16.31.2
 ip route 192.168.33.0/24 172.16.31.2
 omp
  advertise connected
 !
!
```

The device remains vManage-managed; configuration changes are made through the template, while CLI is used only for verification.
