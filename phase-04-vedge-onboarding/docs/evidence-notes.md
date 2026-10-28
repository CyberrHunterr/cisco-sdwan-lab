# Evidence Notes

Phase 4 uses a combination of preserved onboarding material and live CLI verification.

## Current verified edge

The live verification target is **vEdge-PRS2**:

- system IP `55.55.55.51`
- site ID `50`
- organization `appbee-sdwan-project`
- vBond `100.10.1.12`
- chassis `dfb08239-7aff-43eb-a6d3-92eb3c4cdfd9`
- serial `09`

## Current-state warning

The lab has continued into later phases. The current `show running-config vpn 0` output therefore contains OSPF configuration introduced during Phase 5.

That output is still useful as raw current-state evidence, but Phase 4 acceptance is limited to:

- edge system identity,
- transport interfaces,
- Root CA trust,
- valid device certificate,
- chassis/serial identity,
- controller connectivity,
- OMP onboarding.

## Sanitization

Public evidence intentionally removes password hashes and does not preserve private keys, CSR bodies or private certificate material.
