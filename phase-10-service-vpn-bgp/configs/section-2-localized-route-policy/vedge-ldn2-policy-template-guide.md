# vEdge-LDN2 — Localized Route Policy Guide

The Phase 10 Section 2 guide uses vManage Localized Policies for LDN2.

Prefix lists:

- DC-PREFIX: 192.168.36.0/24, 192.168.37.0/24, 192.168.38.0/24
- DRC-PREFIX: 192.168.26.0/24, 192.168.27.0/24, 192.168.28.0/24
- LAN-FACING-PREFIX: 192.168.46.0/24, 192.168.47.0/24, 192.168.48.0/24

SET_LOCALPREF_RECEIVED_PREFIX:

- match DC-PREFIX
- accept
- set local preference 1000
- second rule matches DRC-PREFIX and accepts without modifying local preference
- default action reject

DONT_PASSING_USE_OTHER_PATH:

- match LAN-FACING-PREFIX
- accept
- apply AS-path prepend
- default action reject

Application:

- apply SET_LOCALPREF_RECEIVED_PREFIX outbound toward SITE-LONDON2
- apply DONT_PASSING_USE_OTHER_PATH outbound toward DRC-Cyber2
- attach the localized policy to the London Device Template
- validate Config Preview and push
- verify with:
  - show running-config policy
  - show running-config vpn 2 router bgp
  - show bgp summary

The exact AS-path prepend value used by the final live device is preserved in verification/cli-evidence.
