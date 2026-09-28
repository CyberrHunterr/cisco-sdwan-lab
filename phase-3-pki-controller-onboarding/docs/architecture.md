# Phase 3 — PKI Architecture

## Purpose

The SD-WAN control plane requires device identity to be validated before trusted control connections are established.

Phase 3 introduces a common Root Certificate Authority so that vManage, vBond, vSmart1 and vSmart2 can validate certificates issued from the same trust anchor.

## Trust Model

The lab uses a third-party trust model:

~~~text
                    IOS Root CA
                 CN=rootca.lab.local
                       |
          +------------+------------+
          |            |            |
       vManage        vBond       vSmart1
                                      |
                                   vSmart2
~~~

Each controller receives the Root CA certificate and then receives its own identity certificate after its CSR is signed by the CA.

The controller does not need to directly trust every other controller certificate individually. Instead, the common CA establishes the trust relationship.

## Root CA Parameters

| Parameter | Value |
|---|---|
| Hostname | IOS-Root-CA |
| Address | 100.10.1.100/24 |
| Default next hop | 100.10.1.10 |
| Issuer | CN=rootca.lab.local |
| RSA | 2048-bit |
| Hash | SHA-256 |
| Grant mode | Automatic |
| Root certificate | PKI.ca |
| Distribution service | TFTP |

## Controller Identity

All four controllers use the same SD-WAN organization name:

~~~text
appbee-sdwan-project
~~~

| Controller | System IP | Transport IP |
|---|---|---|
| vManage | 55.55.10.1 | 100.10.1.11 |
| vBond | 55.55.10.2 | 100.10.1.12 |
| vSmart1 | 55.55.10.3 | 100.10.1.13 |
| vSmart2 | 55.55.10.4 | 100.10.1.14 |

Organization-name consistency is important because certificate identity and SD-WAN control-plane identity must agree across the fabric.

## Certificate Lifecycle Used in the Lab

~~~mermaid
sequenceDiagram
    participant C as Controller
    participant CA as IOS Root CA
    participant VM as vManage

    CA->>C: Root certificate (PKI.ca)
    C->>C: Install root certificate chain
    C->>VM: Controller added / CSR generated
    VM->>CA: CSR copied to CA
    CA->>CA: Sign CSR
    CA->>VM: Granted certificate
    VM->>C: Install identity certificate
    C->>C: Certificate state becomes Installed / Valid
~~~

For vManage itself, CSR generation and certificate installation are performed from the vManage certificate workflow.

For vBond and both vSmart instances, vManage is used to add the controller, generate/view the CSR and install the granted certificate.

## Control-Plane Validation

After certificate installation, the controller relationships are verified with:

~~~text
vManage# show control connections
vSmart#  show control connections
vBond#   show orchestrator connections
~~~

The acceptance condition for Phase 3 is that the controller-to-controller DTLS relationships are established and shown as up.

Later vEdge connections are outside Phase 3 scope.
