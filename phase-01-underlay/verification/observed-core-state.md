# Phase 1 — Verification Results

This section summarizes the verification results for the Phase 1 underlay.

Only Phase 1-relevant core adjacencies are included. Later-phase site and edge adjacencies have been intentionally excluded.
> **Evidence note:** PE Router and Internet Router reachability results are based on original Phase 1 records. OSPF/LDP core states for MPLS-P1 through MPLS-P4 were verified from the current lab state and filtered to include only Phase 1-relevant backbone links.

## OSPF Core Adjacencies

| Device | Neighbor | Link / Address | State |
|---|---|---|---|
| PE-ROUTER | MPLS-P1 | 100.1.1.2 | ✅ FULL |
| MPLS-P1 | PE-ROUTER | 100.1.1.1 | ✅ FULL |
| MPLS-P1 | MPLS-P2 | 5.5.5.2 | ✅ FULL |
| MPLS-P1 | MPLS-P3 | 6.6.6.2 | ✅ FULL |
| MPLS-P2 | MPLS-P1 | 5.5.5.1 | ✅ FULL |
| MPLS-P2 | MPLS-P4 | 7.7.7.2 | ✅ FULL |
| MPLS-P3 | MPLS-P1 | 6.6.6.1 | ✅ FULL |
| MPLS-P3 | MPLS-P4 | 8.8.8.2 | ✅ FULL |
| MPLS-P4 | MPLS-P2 | 7.7.7.1 | ✅ FULL |
| MPLS-P4 | MPLS-P3 | 8.8.8.1 | ✅ FULL |

## LDP Sessions

| Device | LDP Peer | Status |
|---|---|---|
| PE-ROUTER | 2.2.2.1 | ✅ Oper |
| MPLS-P1 | PE-ROUTER | ✅ Oper |
| MPLS-P1 | 2.2.2.2 | ✅ Oper |
| MPLS-P1 | 2.2.2.3 | ✅ Oper |
| MPLS-P2 | 2.2.2.1 | ✅ Oper |
| MPLS-P2 | 2.2.2.4 | ✅ Oper |
| MPLS-P3 | 2.2.2.1 | ✅ Oper |
| MPLS-P3 | 2.2.2.4 | ✅ Oper |
| MPLS-P4 | 2.2.2.2 | ✅ Oper |
| MPLS-P4 | 2.2.2.3 | ✅ Oper |

## MPLS Forwarding

The MPLS forwarding tables confirmed that label-switched paths were installed across the provider core.

Example:

```text
MPLS-P2# show mpls forwarding-table

Local      Outgoing   Prefix
Label      Label      or Tunnel Id

18         Pop Label  2.2.2.4/32
19         22         2.2.2.3/32
36         Pop Label  2.2.2.1/32
```

This confirms that MPLS labels are being exchanged and installed for remote core loopbacks. Label values are dynamic and the example reflects the observed lab state.

## Internet Reachability

The Internet Router was validated against the PE router.

```text
internet# ping 100.2.1.1

Success rate is 100 percent (5/5)
```

✅ PE-ROUTER was reachable from the Internet Router.

The PE router default route was also verified:

```text
S* 0.0.0.0/0 via 100.2.1.2
```
## End-to-End Backbone Validation

End-to-end reachability across the MPLS backbone was validated in both directions.

### MPLS-P4 → PE-ROUTER

```text
MPLS-P4# ping 100.1.1.1

Success rate is 100 percent (5/5),
round-trip min/avg/max = 2/8/20 ms
```

Traceroute confirmed that traffic traversed the MPLS backbone:

```text
MPLS-P4# traceroute 100.1.1.1

1  7.7.7.1 [MPLS: Label 38]
   8.8.8.1 [MPLS: Label 34]

2  6.6.6.1
   5.5.5.1

3  100.1.1.1
```

The trace shows successful traversal from MPLS-P4 toward the PE side of the provider backbone.

### PE-ROUTER → MPLS-P4

```text
PE-ROUTER# ping 2.2.2.4

Success rate is 100 percent (5/5),
round-trip min/avg/max = 1/2/4 ms
```

This confirms successful reverse-direction reachability from PE-ROUTER to the MPLS-P4 loopback.

> **Current-state note:** The lab has progressed beyond Phase 1. The current PE-ROUTER traceroute also exposes paths introduced in later phases. For this reason, the ping result is used as Phase 1 end-to-end reachability evidence, while the traceroute is treated as current-state path evidence.

### Result

✅ Bidirectional backbone reachability confirmed.

## Phase 1 Validation Summary

| Test | Result |
|---|---|
| Interface status | ✅ Passed |
| OSPF core adjacency | ✅ Passed |
| LDP adjacency | ✅ Passed |
| MPLS operational state | ✅ Passed |
| MPLS forwarding labels | ✅ Passed |
| PE ↔ Internet Router reachability | ✅ Passed |
| Default route validation | ✅ Passed |
| End-to-end backbone reachability | ✅ Passed |

### Result

**Phase 1 underlay validation completed successfully.**
