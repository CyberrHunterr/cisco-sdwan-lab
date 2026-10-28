# Observed vEdge State

## Identity

| Property | Observed value |
|---|---|
| Hostname | vEdge-PRS2 |
| System IP | 55.55.55.51 |
| Site ID | 50 |
| Organization | appbee-sdwan-project |
| vBond | 100.10.1.12 |
| Chassis ID | dfb08239-7aff-43eb-a6d3-92eb3c4cdfd9 |
| Serial | 09 |

## Transport state

Two WAN interfaces are active:

- `ge0/0` — MPLS — `50.1.2.1/24`
- `ge0/1` — public Internet — `50.2.2.1/24`

## PKI state

`show control local-properties` reports:

- Root CA chain: **Installed**
- Device certificate: **Installed**
- Certificate validity: **Valid**
- Device certificate validity: 17 Aug 2026 → 17 Aug 2027

The root certificate is issued to and by `CN=rootca.lab.local`.

## Control-plane state

The final live vEdge control output showed:

- vSmart1 over MPLS: **up**
- vSmart2 over MPLS: **up**
- vSmart1 over public Internet: **up**
- vSmart2 over public Internet: **up**
- vManage over public Internet: **up**

A live vBond session was also established over public Internet during bring-up.

On vSmart1, the edge was observed over both transports:

- vEdge-PRS2 / MPLS: **up**
- vEdge-PRS2 / public Internet: **up**

vSmart1 also showed active connections to vSmart2, vBond and vManage.

## OMP

`show omp peers` on vSmart1 reported:

- `55.55.55.51` / vedge / site 50: **up**
- `55.55.10.4` / vsmart / site 10: **up**

## Phase boundary

The current edge configuration includes Phase 5 OSPF state. That later state is not used as a Phase 4 acceptance requirement.
