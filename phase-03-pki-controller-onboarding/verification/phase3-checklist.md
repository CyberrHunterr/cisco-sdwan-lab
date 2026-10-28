# Phase 3 — Completion Checklist

## Task 7 — Root CA

- [x] Root CA address defined: 100.10.1.100
- [x] RSA 2048-bit CA key configuration documented
- [x] SHA-256 signing configured
- [x] Issuer configured as CN=rootca.lab.local
- [x] Root certificate export documented
- [x] PKI.ca TFTP distribution documented
- [x] Sensitive CA archive password omitted from the public repository

## Task 8 — vManage Certificate

- [x] Root certificate chain installed
- [x] Identity certificate installed
- [x] Certificate state is Valid
- [x] Organization name is appbee-sdwan-project
- [x] vBond connection is up
- [x] vSmart1 connection is up
- [x] vSmart2 connection is up

## Task 9 — vBond Certificate

- [x] Root certificate chain installed
- [x] Identity certificate installed
- [x] Certificate state is Valid
- [x] Enterprise Root CA observed as CN=rootca.lab.local
- [x] vManage orchestrator relationship is up
- [x] vSmart1 orchestrator relationship is up
- [x] vSmart2 orchestrator relationship is up

## Task 10a — vSmart1 Certificate

- [x] Root certificate chain installed
- [x] Identity certificate installed
- [x] Certificate state is Valid
- [x] vManage connection is up
- [x] vBond connection is up
- [x] vSmart2 connection is up

## Task 10b — vSmart2 Certificate

- [x] Root certificate chain installed
- [x] Identity certificate installed
- [x] Certificate state is Valid
- [x] vManage connection is up
- [x] vBond connection is up
- [x] vSmart1 connection is up

## Task 11 — Controller Onboarding Verification

- [x] vManage controller relationships verified
- [x] vBond orchestrator relationships verified
- [x] vSmart1 controller relationships verified
- [x] vSmart2 controller relationships verified
- [x] All Phase 3 controller-to-controller relationships are up
- [x] Later-phase vEdge rows excluded from Phase 3 acceptance evidence

## Phase Status

**✅ Phase 3 complete — controller PKI trust and onboarding verified.**
