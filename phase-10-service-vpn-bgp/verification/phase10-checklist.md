# Phase 10 Verification Checklist

## Section 1 — iBGP & eBGP

### SITE-LONDON2

- [x] Ethernet0/0 configured as `172.16.42.2`
- [x] Ethernet0/0 UP/UP
- [x] OSPF adjacency with LDN1 FULL
- [x] OSPF adjacency with LDN2 FULL
- [x] BGP AS 65040
- [x] BGP neighbor 40.40.40.1 established
- [x] BGP neighbor 40.40.40.2 established
- [x] `192.168.36.0/24` learned through BGP
- [x] `192.168.37.0/24` learned through BGP
- [x] `192.168.38.0/24` learned through BGP

### vEdge-LDN1

- [x] VPN 2 LAN interface operational
- [x] OSPF neighbors FULL
- [x] iBGP with LDN2 established
- [x] iBGP with SITE-LONDON2 established
- [x] eBGP with DC-DCI established
- [x] loopback-based peers use `update-source loopback0`
- [x] eBGP loopback peer uses `ebgp-multihop 2`

### vEdge-LDN2

- [x] VPN 2 LAN interface operational
- [x] OSPF neighbors FULL
- [x] iBGP with LDN1 established
- [x] iBGP with SITE-LONDON2 established
- [x] eBGP with DC-DCI established
- [x] loopback-based peers use `update-source loopback0`

### vEdge-DC-DCI

- [x] DC2-DCI OSPF adjacency FULL
- [x] iBGP with DC2-DCI established
- [x] eBGP with LDN1 established
- [x] eBGP with LDN2 established
- [x] DC2-DCI iBGP neighbor uses `next-hop-self`

### DC2-DCI

- [x] Ethernet0/0 `172.16.32.2` UP/UP
- [x] OSPF adjacency FULL
- [x] BGP neighbor `30.30.30.1` established
- [x] `192.168.46.0/24` learned through BGP
- [x] `192.168.47.0/24` learned through BGP
- [x] `192.168.48.0/24` learned through BGP

### End-to-end

- [x] London → 192.168.36.10: 5/5
- [x] London → 192.168.37.10: 5/5
- [x] London → 192.168.38.10: 5/5
- [x] DC → 192.168.46.10: 5/5
- [x] DC → 192.168.47.10: 5/5
- [x] DC → 192.168.48.10: 5/5

## Section 2 — Localized Route Policy

### LDN1

- [x] DC-PREFIX list present
- [x] DRC-PREFIX list present
- [x] LAN-FACING-PREFIX list present
- [x] local preference policy present
- [x] DRC prefixes receive local preference 1000
- [x] DC prefixes accepted at default preference
- [x] AS-path prepend policy present
- [x] prepend policy applied toward DC-DCI
- [x] local-preference policy applied toward SITE-LONDON2

### LDN2

- [x] DC-PREFIX list present
- [x] DRC-PREFIX list present
- [x] LAN-FACING-PREFIX list present
- [x] DC prefixes receive local preference 1000
- [x] DRC prefixes accepted at default preference
- [x] prepend policy applied toward DRC-Cyber2
- [x] local-preference policy applied toward SITE-LONDON2

### Policy effect

- [x] SITE-LONDON2 selects DC routes via LDN2 at local preference 1000
- [x] SITE-LONDON2 traceroute to DC uses first hop 172.16.42.3
- [x] DC-DCI selects London prefixes via LDN2
- [x] LDN1 path appears prepended on DC-DCI
- [x] Cyber2 selects London prefixes via LDN1
- [x] LDN2 path appears prepended on Cyber2

## Result

**PASS — Phase 10 Section 1 and Section 2 verified.**
