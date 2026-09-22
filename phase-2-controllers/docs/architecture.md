# Phase 2 Architecture

Phase 1 established the underlay.

Phase 2 adds the four controller instances at Site 10:

```text
vManage   55.55.10.1
vBond     55.55.10.2
vSmart1   55.55.10.3
vSmart2   55.55.10.4
```

All controllers use:

```text
site-id 10
organization-name appbee-sdwan-project
```

Transport addresses:

```text
vManage   100.10.1.11/24
vBond     100.10.1.12/24
vSmart1   100.10.1.13/24
vSmart2   100.10.1.14/24
PE Router 100.10.1.10
```

The current live controller default route points to the PE Router:

```text
0.0.0.0/0 → 100.10.1.10
```

Phase 2 validates the controller base configuration and IP transport. Certificate trust and onboarding are intentionally separated into Phase 3.
