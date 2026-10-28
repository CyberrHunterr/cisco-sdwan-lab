# Evidence Notes

Phase 6 uses both GUI and CLI evidence.

## GUI evidence

GUI screenshots are the primary evidence for:

- Feature Template creation
- Device Template creation
- Device Specific values
- successful push task
- device In Sync state

## CLI evidence

CLI output is used to verify post-push health.

The preserved post-push output confirms:

- vManaged = true
- configuration template = WG3-vEdge-Template
- System state = GREEN
- system identity preserved
- VPN 0 OSPF point-to-point preserved
- controller connections UP
- BFD sessions UP
- OMP peers UP
- MPLS OSPF adjacency FULL

## Phase boundary

A later Service VPN OSPF neighbor is visible in the current CLI state. It is excluded from Phase 6 acceptance because Service VPN work belongs to later phases.
