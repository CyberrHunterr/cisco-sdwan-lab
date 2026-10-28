# vEdge-LDN2 — Guide Template Workflow

The Phase 10 guide prescribes vManage templates rather than a handwritten full CLI configuration for LDN2.

Required design:

- copy the Paris site templates; do not edit the originals
- create London Service VPN 2
- LAN addressing for the guide baseline: 172.16.42.2/24
- VRRP group 40, with priority lower than LDN1
- loopback0: 40.40.40.2/24
- VPN 2 OSPF with administrative distance 210
- include loopback0 in OSPF
- BGP AS 65040
- iBGP neighbors:
  - 40.40.40.1 (LDN1)
  - 40.40.40.100 (SITE-LONDON2)
- enable Next-Hop Self on iBGP peers
- use loopback as source
- during the iBGP stage, redistribute OMP into BGP
- during Task 46, remove redistribute OMP and add eBGP neighbor 30.30.30.1
- eBGP uses remote-as 65030 and ebgp-multihop 2
- verify Config Preview before push
- verify with show running-config vpn 2, show ospf neighbor, show bgp summary and show vrrp

The final live state can differ from the guide's initial working values; verified operational state is preserved under verification/cli-evidence.
