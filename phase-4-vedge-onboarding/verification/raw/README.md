# Phase 4 Raw Evidence

This directory preserves real CLI evidence captured from the running lab.

Files:

- `vedge-prs2-show-output.txt` — selected vEdge-PRS2 configuration, PKI and control-plane output
- `vsmart1-show-output.txt` — final vSmart1 OMP and control-connection output

## Evidence rules

- Output is preserved as observed where practical.
- Password hashes and other authentication secrets are removed.
- Certificate public metadata may remain because it is not private-key material.
- Later-phase state may appear in raw output because the lab progressed after Phase 4.
- No missing CLI output is fabricated.
