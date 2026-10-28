# PRS2 Device Template

Phase 8 moves **vEdge-PRS2** to vManage template management using a Device Template dedicated to the Paris branch.

Recommended/observed template role:

- Device: `vEdge-PRS2`
- System IP: `55.55.55.51`
- Site ID: `50`
- Device Template: PRS2-specific template
- Service VPN: VPN 1
- LAN interface: `ge0/2`

The PRS2 template is intentionally separate from the DCI Device Template so that Paris VRRP/DHCP changes do not propagate to the data-center device.

Post-push verification confirms controller connections and BFD sessions remain operational.
