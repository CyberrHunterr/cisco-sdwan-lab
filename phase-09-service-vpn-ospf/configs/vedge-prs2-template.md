# vEdge-PRS2 — VPN 1 OSPF Template Intent

Phase 9 extends the existing Paris PRS2 Device Template rather than creating a separate standalone device configuration.

## OSPF values

- Router ID: `55.55.55.51`
- Default route origination: enabled
- Redistribute: OMP
- Area: `0`
- Interface: `ge0/2`
- Cost: `6`

Resulting device configuration observed in the preserved screenshot:

```text
vpn 1
 router
  ospf
   router-id 55.55.55.51
   default-information originate
   timers spf 200 1000 10000
   redistribute omp
   area 0
    interface ge0/2
     cost 6
    exit
   exit
  !
 !
```

The same running configuration also retains the Phase 8 VRRP and DHCP configuration under `ge0/2`.

The template workflow is evidenced by:

- OSPF Config Diff screenshot
- vManage Push Feature Template Configuration — Success screenshot
- post-push running configuration
- post-push OSPF neighbor and route-table verification
