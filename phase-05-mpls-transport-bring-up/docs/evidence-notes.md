# Evidence Notes

Phase 5 evidence is based on live CLI output captured from:

- vEdge-PRS2
- vEdge-DC-DCI
- MPLS-P3
- Internet Router

## Strongest verified chain

1. MPLS-P3 forms a FULL OSPF adjacency with Internet Router over `3.3.3.0/30`.
2. vEdge-PRS2 forms a FULL OSPF adjacency on its MPLS-facing interface.
3. vEdge-PRS2 learns MPLS/core/transport routes through OSPF.
4. vEdge-PRS2 establishes controller sessions over MPLS.
5. PRS2↔DCI forms all four BFD transport combinations.

## Limitation

vEdge-DC-DCI still showed DOWN BFD sessions toward `55.55.55.40`.

This means the evidence supports successful **core bring-up and verified cross-transport BFD on the PRS2↔DCI path**, but not a claim that every edge-to-edge BFD session in the complete topology was healthy at capture time.
