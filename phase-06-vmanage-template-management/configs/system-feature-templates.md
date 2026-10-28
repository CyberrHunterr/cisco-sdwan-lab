# System Feature Templates

Phase 6 uses the following Basic Information feature templates for vEdge-DC-DCI:

- WG3-System
- WG3-System-AAA
- WG3-System-BFD
- WG3-System-OMP
- WG3-System-Security

## WG3-System

Device-specific values:

- Hostname: `vEdge-DC-DCI`
- System IP: `55.55.55.30`
- Site ID: `30`

Global/shared values preserved from the existing device/fabric:

- Organization name: `appbee-sdwan-project`
- vBond: `100.10.1.12`

The Phase 6 workflow intentionally marks Hostname, System IP and Site ID as **Device Specific**, while values shared across devices remain global.

## AAA / BFD / OMP / Security

These templates are included so that the Device Template fully represents the existing device configuration instead of leaving Basic Information blocks unassigned.

The lab workflow uses the existing/default behavior for these templates unless a value is explicitly required by the current device configuration.
