# Phase 8 Verification Checklist

| Check | PRS1 | PRS2 |
|---|---:|---:|
| VPN 1 LAN interface configured | ✅ | ✅ |
| LAN IP correct | ✅ | ✅ |
| VRRP group 50 configured | ✅ | ✅ |
| VRRP virtual IP 172.16.51.254 | ✅ | ✅ |
| Track OMP enabled | ✅ | ✅ |
| OMP state UP | ✅ | ✅ |
| PRS1 primary / PRS2 backup | ✅ | ✅ |
| DHCP server configured | ✅ | ✅ |
| DHCP pool 172.16.51.0/24 | ✅ | ✅ |
| VRRP VIP used as DHCP gateway | ✅ | ✅ |
| DNS 8.8.8.8 configured | ✅ | ✅ |
| DHCP server operational evidence | ✅ | ✅ |
| DHCP lease observed | — | ✅ |
| PRS2 control connections healthy after template work | — | ✅ |
| PRS2 BFD healthy after template work | — | ✅ |
| Failover: PRS2 promoted to primary after PRS1 LAN shutdown | ⬜ | ⬜ |
| Failover packet-loss measurement preserved | ⬜ | ⬜ |
| Post-test roles restored | ⬜ | ⬜ |

## Current result

**VRRP configuration: PASS**

**DHCP configuration: PASS**

**Template post-change health: PASS**

**Final failover acceptance: PENDING preserved evidence**
