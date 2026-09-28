# Phase 3 — PKI and Controller Onboarding

## Objective

Phase 3 establishes certificate-based trust between the SD-WAN controllers deployed in Phase 2.

The scope of this phase is:

- configure an IOS-based Root Certificate Authority,
- distribute the enterprise root certificate to the controllers,
- generate and sign controller CSRs,
- install identity certificates on vManage, vBond, vSmart1 and vSmart2,
- verify that the controller control-plane relationships are established.

## Controller Identity

| Controller | System IP | Transport IP | Organization |
|---|---|---|---|
| vManage | 55.55.10.1 | 100.10.1.11 | appbee-sdwan-project |
| vBond | 55.55.10.2 | 100.10.1.12 | appbee-sdwan-project |
| vSmart1 | 55.55.10.3 | 100.10.1.13 | appbee-sdwan-project |
| vSmart2 | 55.55.10.4 | 100.10.1.14 | appbee-sdwan-project |

## Root Certificate Authority

The Root CA used for the lab is based on IOS and uses:

| Setting | Value |
|---|---|
| CA address | 100.10.1.100 |
| Hostname | IOS-Root-CA |
| Issuer | CN=rootca.lab.local |
| RSA key size | 2048 bits |
| Hash algorithm | SHA-256 |
| Root certificate file | PKI.ca |
| Distribution | TFTP |

Public CA configuration:

➡️ [configs/root-ca.cfg](configs/root-ca.cfg)

Sensitive archive passwords and private-key material are intentionally not published.

## Trust Workflow

~~~mermaid
flowchart TD
    CA[IOS Root CA<br/>CN=rootca.lab.local]
    VM[vManage]
    VB[vBond]
    VS1[vSmart1]
    VS2[vSmart2]

    CA -->|Root certificate| VM
    CA -->|Root certificate| VB
    CA -->|Root certificate| VS1
    CA -->|Root certificate| VS2

    VM -->|CSR| CA
    VB -->|CSR| CA
    VS1 -->|CSR| CA
    VS2 -->|CSR| CA

    CA -->|Signed identity certificate| VM
    CA -->|Signed identity certificate| VB
    CA -->|Signed identity certificate| VS1
    CA -->|Signed identity certificate| VS2
~~~

The onboarding sequence for each controller is:

~~~text
Install Root CA certificate
        ↓
Generate CSR
        ↓
Sign CSR on Root CA
        ↓
Install identity certificate
        ↓
Verify certificate state
        ↓
Verify DTLS control connections
~~~

Detailed workflow:

➡️ [docs/controller-certificate-workflow.md](docs/controller-certificate-workflow.md)

## Verification Results

Current controller CLI state confirms that all four controllers retain the enterprise root chain and valid identity certificates.

| Controller | Root CA Chain | Identity Certificate | Controller Peers |
|---|---|---|---|
| vManage | ✅ Installed | ✅ Valid | vBond, vSmart1, vSmart2 up |
| vBond | ✅ Installed | ✅ Valid | vManage, vSmart1, vSmart2 up |
| vSmart1 | ✅ Installed | ✅ Valid | vManage, vBond, vSmart2 up |
| vSmart2 | ✅ Installed | ✅ Valid | vManage, vBond, vSmart1 up |

Detailed evidence:

➡️ [verification/observed-controller-state.md](verification/observed-controller-state.md)

Completion checklist:

➡️ [verification/phase3-checklist.md](verification/phase3-checklist.md)

## Scope Note

The live lab has progressed beyond Phase 3 and therefore contains vEdge control connections created in later phases.

Phase 3 verification intentionally filters the live output to the four controller relationships only.

## Phase Result

**Phase 3 PKI trust establishment and controller onboarding completed successfully.**

The next phase introduces vEdge certificate installation and edge onboarding into the SD-WAN fabric.
