# vEdge-DC-DCI — Guide Template Workflow

The Phase 10 guide prescribes a vManage template workflow for DC-DCI.

Required design:

- copy LDN2 VPN 2 feature templates and remove London-specific values
- do not use VRRP on the DC LAN because there is only one vEdge
- add VPN 2 OSPF and BGP to the existing DC-DCI Device Template
- keep prior VPN 0, VPN 1 and VPN 512 configuration intact
- BGP AS 65030
- local iBGP peer: DC2-DCI at 30.30.30.100
- London eBGP peers use ebgp-multihop 2
- the guide explicitly states not to use Next-Hop Self on London eBGP neighbors
- validate the Config Preview before push
- verify with show bgp summary and show ip route vpn 2

Operational troubleshooting later required next-hop handling on the DC-side iBGP path; see docs/troubleshooting.md and verification/cli-evidence for the final live state.
