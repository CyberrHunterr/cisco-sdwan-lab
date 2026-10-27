# CLI vs Template Comparison

Phase 7 deliberately implements the same Service VPN outcome through two different management methods.

| Property | Cyber2 | DCI |
|---|---|---|
| Device | vEdge-DRC-Cyber2 | vEdge-DC-DCI |
| System IP | 55.55.55.20 | 55.55.55.30 |
| Method | CLI | vManage Template |
| VPN | 1 | 1 |
| LAN interface | ge0/3 | ge0/3 |
| LAN IP | 172.16.21.1/24 | 172.16.31.1/24 |
| Local connected route | 172.16.21.0/24 | 172.16.31.0/24 |
| Static routes | 192.168.21-23.0/24 | 192.168.31-33.0/24 |
| OMP peers | UP | UP |
| Remote routes learned via OMP | Yes | Yes |
| Cross-site ping | Success | Success |
| Cross-site traceroute | Success | Success |

## Result

Operationally, the forwarding and control-plane output does not identify whether the configuration was entered manually through CLI or generated through vManage templates.

The difference is the management source, not the resulting network behavior.
