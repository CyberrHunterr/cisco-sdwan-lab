# Phase 1 Architecture

## Why the Underlay Comes First

Before the SD-WAN control plane can be introduced, the underlying transport network must be reachable and stable.

Phase 1 therefore focuses on the provider-side and Internet-side underlay rather than SD-WAN policy or controller onboarding.

## Routing

OSPF Area 0 is used to exchange reachability across the provider core.

The retained Phase 1 core path is:

```text
PE-ROUTER
   |
MPLS-P1
 /     \
P2     P3
 \     /
  MPLS-P4
```

This creates more than one core path between parts of the provider network.

## MPLS and LDP

MPLS forwarding is enabled across the Phase 1 core.

LDP distributes labels between the core routers. Loopback interfaces on P1–P4 provide stable router identifiers for the label distribution process.

## Internet Handoff

PE-ROUTER uses the Internet Router as its default path for unknown destinations.

Historical Phase 1 evidence records:

```text
ip route 0.0.0.0 0.0.0.0 100.2.1.2
```

The Internet Router itself used its external-facing interface as the default route during the original Phase 1 implementation.

## Validation Principle

Configuration alone is not treated as completion.

The backbone is validated using:

- OSPF neighbor state,
- LDP neighbor state,
- MPLS interface state,
- MPLS forwarding table,
- ping,
- traceroute.
