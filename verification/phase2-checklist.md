# Phase 2 Verification Checklist

## Controller System Configuration

Run on vBond, vSmart1, vSmart2 and vManage:

```text
show running-config system
show running-config vpn
show interface
show ip route
show arp
```

Verify:

- hostname
- system IP
- site ID
- organization name
- vBond address
- VPN 0 interface
- VPN 512 interface
- default route

## Reachability

### vSmart1 / vSmart2

```text
ping 100.10.1.10
ping 100.10.1.12
```

### vManage

```text
ping 100.10.1.10
ping 100.10.1.12
ping 100.10.1.13
ping 100.10.1.14
```

### vBond

```text
ping 100.10.1.10
ping 100.10.1.11
ping 100.10.1.13
ping 100.10.1.14
```

## GUI

Verify:

- vManage GUI loads over HTTPS
- controller inventory lists vManage, vBond, vSmart1 and vSmart2

## Phase Boundary

Do not use certificate installation, trust establishment or final control-connection status as Phase 2 completion criteria. Those belong to Phase 3.
