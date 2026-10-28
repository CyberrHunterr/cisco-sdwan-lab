# Phase 10 Configuration Set

The Phase 10 Word guides are the **design/configuration source of truth**.

This directory therefore separates two things:

- **guide-reference** files reproduce the CLI configuration or template workflow prescribed by the Phase 10 guides.
- the existing device `.conf` files preserve the **final observed lab state** used during verification after troubleshooting.

This distinction matters because the live lab required a few corrections and used some values that differ from the initial working table in the guide.

## Section 1 — iBGP & eBGP

- `section-1-ibgp-ebgp/site-london2-guide.cfg` — Task 43 CLI configuration from the guide
- `section-1-ibgp-ebgp/dc2-dci-guide.cfg` — Task 43 CLI configuration from the guide
- `section-1-ibgp-ebgp/vedge-ldn1-guide.cfg` — Task 44a + Task 46 CLI configuration from the guide
- `section-1-ibgp-ebgp/vedge-ldn2-template-guide.md` — template workflow from the guide
- `section-1-ibgp-ebgp/vedge-dc-dci-template-guide.md` — template workflow from the guide

## Section 2 — Localized Route Policy

- `section-2-localized-route-policy/vedge-ldn1-policy-guide.cfg` — CLI policy from the guide
- `section-2-localized-route-policy/vedge-ldn2-policy-template-guide.md` — vManage localized-policy workflow from the guide

## Verification

Operational evidence and the final live state are kept under:

- `../verification/cli-evidence/`
- `../docs/troubleshooting.md`

The repository does not treat the guide's initial addressing table as more authoritative than the final verified device state when the two differ.
