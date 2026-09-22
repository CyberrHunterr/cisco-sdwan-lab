# Observed Core State

This file separates **historical Phase 1 evidence** from **later live captures**.

The later captures were taken after the lab had progressed to a later phase. Only Phase 1-relevant core adjacencies are summarized here.

## Historical Phase 1 Evidence

### PE-ROUTER

The original Phase 1 work recorded:

- default route via `100.2.1.2`,
- OSPF adjacency between PE-ROUTER and MPLS-P1 in `FULL` state,
- MPLS interfaces operational,
- LDP adjacency to MPLS-P1 established,
- successful ping to `100.2.1.2`,
- traceroute to `100.2.1.2` reaching the directly connected target.

### Internet Router

The original Phase 1 work recorded:

- default route through `Ethernet2/0`,
- route table validation,
- successful `5/5` ICMP test to PE-ROUTER `100.2.1.1`.

## Later Live Capture — Filtered to Phase 1 Core

| Device | OSPF core neighbors retained for Phase 1 | State |
|---|---|---|
| PE-ROUTER | MPLS-P1 (`100.1.1.2`) | FULL |
| MPLS-P1 | PE, P2 (`5.5.5.2`), P3 (`6.6.6.2`) | FULL |
| MPLS-P2 | P1 (`5.5.5.1`), P4 (`7.7.7.2`) | FULL |
| MPLS-P3 | P1 (`6.6.6.1`), P4 (`8.8.8.2`) | FULL |
| MPLS-P4 | P2 (`7.7.7.1`), P3 (`8.8.8.1`) | FULL |

The live captures also showed operational LDP sessions on these core links.

Examples retained from the current state:

```text
PE-ROUTER -> MPLS-P1
OSPF: FULL
LDP peer: 2.2.2.1:0
LDP state: Oper
```

```text
MPLS-P1 -> MPLS-P2 / MPLS-P3
OSPF: FULL
LDP peers: 2.2.2.2:0, 2.2.2.3:0
LDP state: Oper
```

```text
MPLS-P2 -> MPLS-P1 / MPLS-P4
OSPF: FULL
LDP peers: 2.2.2.1:0, 2.2.2.4:0
LDP state: Oper
```

```text
MPLS-P3 -> MPLS-P1 / MPLS-P4
OSPF: FULL
LDP peers: 2.2.2.1:0, 2.2.2.4:0
LDP state: Oper
```

```text
MPLS-P4 -> MPLS-P2 / MPLS-P3
OSPF: FULL
LDP peers: 2.2.2.2:0, 2.2.2.3:0
LDP state: Oper
```

## Excluded From Phase 1 Evidence

Later live captures contain additional site-facing OSPF neighbors, Internet-side core paths, static routes and transport networks.

Those are not treated as Phase 1 proof unless a Phase 1-period source confirms them.
