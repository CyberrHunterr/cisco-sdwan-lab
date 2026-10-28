# Phase 10 Troubleshooting

This file records the implementation corrections that led to the final working Phase 10 state.

## SITE-LONDON2 LAN interface

The London LAN-facing router interface required completion of its IP configuration and activation.

Final observed state:

- Ethernet0/0: `172.16.42.2`
- interface state: UP/UP

## OSPF network type

LAN-facing Ethernet OSPF interfaces in the London and DC segments were corrected to use normal broadcast Ethernet behavior rather than point-to-point behavior.

Final result:

- SITE-LONDON2 forms FULL adjacency with LDN1 and LDN2
- DC2-DCI forms FULL adjacency with DC-DCI

Loopback interfaces remain suitable for loopback reachability and BGP peering.

## BGP update-source

Loopback-based BGP sessions require the BGP source to match the configured loopback neighbor address.

Missing `update-source loopback0` statements were added where required.

Final result:

- London iBGP peers established
- London ↔ DC eBGP peers established
- London ↔ Cyber2 eBGP peers established

## DC next-hop handling

The DC LAN-side iBGP relationship required `next-hop-self` so DC2-DCI could receive London routes with a reachable next hop.

Final observed DC-DCI configuration includes:

```text
neighbor 30.30.30.100
 remote-as 65030
 update-source loopback0
 next-hop-self
```

## Final validation

After the corrections:

- SITE-LONDON2 learned `192.168.36/37/38.0/24` through BGP
- DC2-DCI learned `192.168.46/47/48.0/24` through BGP
- all six final sourced ping tests completed 5/5
- end-to-end reachability was 100%

Section 2 route policy also produced the intended path selection:

- London → DC prefers LDN2
- DC → London prefers LDN2
- Cyber2 → London prefers LDN1
