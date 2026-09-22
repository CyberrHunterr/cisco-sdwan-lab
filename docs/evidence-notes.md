# Phase 2 Evidence Notes

## Evidence Used

This public reconstruction uses:

- the original Phase 2 guide,
- historical controller reports,
- current live CLI output from vBond, vSmart1, vSmart2 and vManage,
- current vManage GUI screenshots.

## Current vs Historical Default Gateway

Historical Phase 2 reports referenced:

```text
100.10.1.254
```

as the controller default gateway.

The current live configuration on all four controllers uses:

```text
100.10.1.10
```

which is the PE Router transport address.

The public configuration files preserve the current live value and document the historical difference here.

## vBond VPN 512

The historical vBond report did not contain a complete VPN 512 configuration block.

The current live CLI now confirms:

```text
vpn 512
 interface eth0
  ip address 100.10.1.12/24
  no shutdown
```

Therefore VPN 512 is now marked as verified for vBond.

## Authentication Data

Password hashes and authentication secrets were removed from all public configuration files.

## Later-Phase State

The current vManage GUI shows certificate and synchronization information created in later phases.

Those fields are intentionally excluded from Phase 2 acceptance criteria.
