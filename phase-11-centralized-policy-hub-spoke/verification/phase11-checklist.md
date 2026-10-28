# Phase 11 Verification Checklist

## vSmart control plane

- [x] vSmart1 control connections UP
- [x] vSmart2 control connections UP
- [x] vSmart1 centralized policy present
- [x] vSmart1 apply-policy present
- [x] vSmart2 centralized policy present
- [x] vSmart2 apply-policy present

## Centralized policy

- [x] HO-HUB site list contains Site 1
- [x] PRS-DRC-SPOKE contains Sites 20 and 50
- [x] VPN1 contains VPN 1
- [x] HUB-HO-TLOC contains 55.55.55.1 / mpls / ipsec
- [x] HS-PRS-DRC control policy present
- [x] default-action reject present
- [x] policy applied to hub and spoke site lists

## Hub correction

- [x] Head Office VPN 1 static default route points to Null0
- [x] static routes advertised into OMP

## Spoke route state

- [x] Paris spoke learns 0.0.0.0/0 through OMP
- [x] Paris spoke uses hub TLOC 55.55.55.1
- [x] DRC spoke learns 0.0.0.0/0 through OMP
- [x] DRC spoke uses hub TLOC 55.55.55.1

## Path validation

- [x] Paris → DRC traceroute traverses Head Office
- [x] DRC → Paris traceroute traverses Head Office

## Result

**PASS — Phase 11 centralized Hub & Spoke behavior verified.**

**Program status: 11 / 11 phases complete.**
