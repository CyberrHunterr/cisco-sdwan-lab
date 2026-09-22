# Phase 2 — SD-WAN Controller Deployment

## Objective

Phase 2 builds the SD-WAN controller layer on top of the Phase 1 underlay.

The scope of this phase is limited to the base configuration and IP-level validation of:

- vBond
- vSmart1
- vSmart2
- vManage

Certificate installation and controller onboarding are intentionally treated as Phase 3 work.

## Controller Identity

| Controller | System IP | Site ID | Organization |
|---|---|---:|---|
| vManage | 55.55.10.1 | 10 | appbee-sdwan-project |
| vBond | 55.55.10.2 | 10 | appbee-sdwan-project |
| vSmart1 | 55.55.10.3 | 10 | appbee-sdwan-project |
| vSmart2 | 55.55.10.4 | 10 | appbee-sdwan-project |

## Transport and Management Networks

| Controller | VPN 0 | VPN 512 |
|---|---|---|
| vManage | 100.10.1.11/24 | 100.10.1.11/24 |
| vBond | 100.10.1.12/24 | 100.10.1.12/24 |
| vSmart1 | 100.10.1.13/24 | 100.10.1.13/24 |
| vSmart2 | 100.10.1.14/24 | 100.10.1.14/24 |

The current live lab uses the PE Router transport address `100.10.1.10` as the default next hop.

## Verification Results

| Validation | Status |
|---|---|
| Controller system identities | ✅ Passed |
| VPN 0 transport interfaces | ✅ Passed |
| VPN 512 management interfaces | ✅ Passed |
| Default routing | ✅ Passed |
| vSmart1 → PE Router / vBond | ✅ Passed |
| vSmart2 → PE Router / vBond | ✅ Passed |
| vManage → PE Router / controllers | ✅ Passed |
| vManage GUI access | ✅ Passed |
| Controller inventory visibility | ✅ Passed |

## Scope Note

Phase 2 covers controller base configuration and IP-level reachability.

Certificate installation, trust establishment and controller onboarding are documented separately in Phase 3.
