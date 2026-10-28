# Phase 8 — Service VPN: VRRP & DHCP

Phase 8 adds branch gateway redundancy and DHCP services to the Paris branch (Site ID 50).

Two configuration methods are used:

- **vEdge-PRS1 (55.55.55.50)** — CLI-managed
- **vEdge-PRS2 (55.55.55.51)** — vManage template-managed

## Working values

- VPN: `1`
- LAN segment: `172.16.51.0/24`
- LAN interface: `ge0/2`
- VRRP group: `50`
- Virtual IP: `172.16.51.254`
- PRS1 IP: `172.16.51.1/24`
- PRS1 priority: `200`
- PRS2 IP: `172.16.51.2/24`
- PRS2 priority: `150`

## DHCP

Both devices use:

- address pool: `172.16.51.0/24`
- excluded addresses:
  - `172.16.51.1`
  - `172.16.51.2`
  - `172.16.51.254`
  - `172.16.51.3`
- offer time: `600`
- lease time: `86400`
- default gateway: `172.16.51.254`
- DNS: `8.8.8.8`

## Verified state

### PRS1

- VRRP state: **primary**
- priority: **200**
- OMP state: **up**
- DHCP server configured and enabled
- no current DHCP binding on PRS1

### PRS2

- VRRP state: **backup**
- priority: **150**
- OMP state: **up**
- DHCP server configured and enabled
- active DHCP binding: `172.16.51.69`
- vSmart/vManage control connections: **UP**
- verified BFD sessions: **UP**

## Scope note

Current device output also contains routing configuration introduced by later work, including VPN 1 OSPF. Those later-phase elements are preserved in device state but are excluded from Phase 8 acceptance criteria.

## Evidence

- [configs/](configs/)
- [verification/device-verification/vedge-prs1-vrrp-dhcp.txt](verification/device-verification/vedge-prs1-vrrp-dhcp.txt)
- [verification/device-verification/vedge-prs2-vrrp-dhcp.txt](verification/device-verification/vedge-prs2-vrrp-dhcp.txt)
- [verification/phase8-checklist.md](verification/phase8-checklist.md)

## Phase status

**VRRP + DHCP configuration: ✅ Verified**

**Failover acceptance: ⬜ Pending preserved failover evidence**
