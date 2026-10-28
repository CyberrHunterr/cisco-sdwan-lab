# VPN 0 OSPF Feature Template

The OSPF feature template is required so that the Phase 5 MPLS routing configuration is not removed during the Device Template push.

Configured values:

- VPN: `0`
- Router ID: `55.55.55.30`
- SPF timers: `200 1000 10000`
- Area: `0`
- Interface: `ge0/1`
- Network type: `point-to-point`

Final post-push CLI verification confirmed that the `network point-to-point` setting was preserved.
