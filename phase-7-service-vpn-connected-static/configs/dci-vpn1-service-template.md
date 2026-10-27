# DCI VPN 1 Service Feature Template

Target device: `vEdge-DC-DCI`

Feature template:

- Template role: Service VPN
- VPN ID: `1`
- Example/working template name: `WG3-VPN1-Service`

## Connected route advertisement

The VPN 1 configuration preserves:

```text
vpn 1
 omp
  advertise connected
 !
!
```

## Static routes

The template contains:

| Prefix | Next Hop |
|---|---|
| 192.168.31.0/24 | 172.16.31.2 |
| 192.168.32.0/24 | 172.16.31.2 |
| 192.168.33.0/24 | 172.16.31.2 |

Post-push verification confirms these routes are installed as static routes and their remote copies are propagated through OMP.
