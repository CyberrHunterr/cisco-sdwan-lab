# Phase 1 Verification Checklist

A Phase 1 device is not considered complete only because the configuration was entered. The underlay must be verified.

## Internet Router

```text
show ip interface brief
show ip route
ping 100.2.1.1
```

Expected:

- public-facing interface obtains an address via DHCP,
- a default route exists,
- PE-ROUTER is reachable.

## PE-ROUTER

```text
show ip interface brief
show ip route
show ip ospf neighbor
show mpls interfaces
show mpls ldp neighbor
show mpls forwarding-table
ping 100.2.1.2
traceroute 100.2.1.2
```

Expected:

- default route points toward the Internet Router,
- OSPF adjacency to the MPLS core is FULL,
- MPLS is operational on the Phase 1 MPLS-facing path,
- LDP adjacency is operational.

## MPLS-P1 / P2 / P3 / P4

```text
show ip interface brief
show ip route
show ip ospf neighbor
show mpls interfaces
show mpls ldp neighbor
show mpls forwarding-table
```

Expected:

- all core OSPF neighbors are FULL,
- all intended core LDP peers are in `Oper` state,
- MPLS forwarding entries exist for remote core loopbacks.

## End-to-End Core Test

Recommended final Phase 1 evidence:

```text
ping <remote-core-loopback>
traceroute <remote-core-loopback>
```

Run from both sides of the core where possible.
