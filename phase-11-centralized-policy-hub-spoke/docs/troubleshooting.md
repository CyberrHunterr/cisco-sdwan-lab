# Phase 11 Troubleshooting

## Initial state

The vSmart control connections were operational, but centralized policy was initially absent:

```text
show running-config policy
% No entries found.

show running-config apply-policy
% No entries found.
```

This indicated that the controller fabric itself was healthy, while the centralized control policy had not yet been installed.

## Centralized policy state

The final configuration contains:

- `HO-HUB` — Site 1
- `PRS-DRC-SPOKE` — Sites 20 and 50
- `VPN1` — VPN 1
- `HUB-HO-TLOC` — 55.55.55.1 / mpls / ipsec
- `HS-PRS-DRC` control policy
- `default-action reject`

The policy is applied outbound to the hub and spoke site lists.

The same policy and apply-policy state is present on vSmart1 and vSmart2.

## Unreachable spoke behavior

After Hub & Spoke policy enforcement, direct spoke-to-spoke route visibility is intentionally restricted.

To restore controlled spoke-to-spoke forwarding through the hub, Head Office advertises a default route.

Final hub configuration:

```text
vpn 1
 ip route 0.0.0.0/0 null0
 omp
  advertise static
 !
!
```

The Null0 default prevents unknown destinations from looping indefinitely at the hub.

## Final result

The spoke routers learn a default route through OMP with Head Office as the TLOC.

Observed path behavior:

- Paris → DRC traverses Head Office
- DRC → Paris traverses Head Office
- centralized policy is present on both vSmart controllers
- controller connections remain UP
