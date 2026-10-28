# Phase 3 — Controller PKI Verification

This file summarizes current live evidence relevant to Phase 3.

The lab has progressed beyond controller onboarding, so later vEdge sessions are excluded from this phase-specific view.

## Certificate State

### vManage

~~~text
personality                       vmanage
organization-name                 appbee-sdwan-project
root-ca-chain-status              Installed
root-ca-crl-status                Installed
certificate-status                Installed
certificate-validity              Valid
certificate-not-valid-before      Aug 13 08:10:24 2026 GMT
certificate-not-valid-after       Aug 13 08:10:24 2027 GMT
system-ip                         55.55.10.1
~~~

### vBond

~~~text
personality                       vedge
organization-name                 appbee-sdwan-project
root-ca-chain-status              Installed
root-ca-crl-status                Installed
certificate-status                Installed
certificate-validity              Valid
certificate-not-valid-before      Aug 13 18:12:31 2026 GMT
certificate-not-valid-after       Aug 13 18:12:31 2027 GMT
system-ip                         55.55.10.2
~~~

### vSmart1

~~~text
personality                       vsmart
organization-name                 appbee-sdwan-project
root-ca-chain-status              Installed
root-ca-crl-status                Installed
certificate-status                Installed
certificate-validity              Valid
certificate-not-valid-before      Aug 13 19:24:52 2026 GMT
certificate-not-valid-after       Aug 13 19:24:52 2027 GMT
system-ip                         55.55.10.3
~~~

### vSmart2

~~~text
personality                       vsmart
organization-name                 appbee-sdwan-project
root-ca-chain-status              Installed
root-ca-crl-status                Installed
certificate-status                Installed
certificate-validity              Valid
certificate-not-valid-before      Aug 13 19:56:15 2026 GMT
certificate-not-valid-after       Aug 13 19:56:15 2027 GMT
system-ip                         55.55.10.4
~~~

## Certificate Summary

| Controller | System IP | Root Chain | Identity Certificate | Valid Until |
|---|---|---|---|---|
| vManage | 55.55.10.1 | ✅ Installed | ✅ Valid | 2027-08-13 08:10:24 GMT |
| vBond | 55.55.10.2 | ✅ Installed | ✅ Valid | 2027-08-13 18:12:31 GMT |
| vSmart1 | 55.55.10.3 | ✅ Installed | ✅ Valid | 2027-08-13 19:24:52 GMT |
| vSmart2 | 55.55.10.4 | ✅ Installed | ✅ Valid | 2027-08-13 19:56:15 GMT |

## Enterprise Root CA Observed on vBond

~~~text
Version: 3
Serial Number: 1
Signature Algorithm: sha256WithRSAEncryption
Issuer: CN=rootca.lab.local
Subject: CN=rootca.lab.local
RSA Public-Key: 2048 bit
X509v3 Basic Constraints: CA:TRUE
~~~

Observed validity:

~~~text
Not Before: Aug 11 19:28:20 2026 GMT
Not After : Aug 10 19:28:20 2029 GMT
~~~

## vManage Controller Connections

Phase 3-relevant rows from show control connections:

~~~text
PEER TYPE  PROT  SYSTEM IP    PUBLIC IP      ORGANIZATION           STATE
vsmart     dtls  55.55.10.3   100.10.1.13   appbee-sdwan-project   up
vsmart     dtls  55.55.10.4   100.10.1.14   appbee-sdwan-project   up
vbond      dtls  55.55.10.2   100.10.1.12   appbee-sdwan-project   up
~~~

✅ vManage has active DTLS relationships with vBond, vSmart1 and vSmart2.

## vSmart1 Controller Connections

Phase 3-relevant rows:

~~~text
PEER TYPE  PROT  SYSTEM IP    PUBLIC IP      ORGANIZATION           STATE
vsmart     dtls  55.55.10.4   100.10.1.14   appbee-sdwan-project   up
vbond      dtls  55.55.10.2   100.10.1.12   appbee-sdwan-project   up
vmanage    dtls  55.55.10.1   100.10.1.11   appbee-sdwan-project   up
~~~

✅ vSmart1 has active DTLS relationships with vSmart2, vBond and vManage.

## vSmart2 Controller Connections

Phase 3-relevant rows:

~~~text
PEER TYPE  PROT  SYSTEM IP    PUBLIC IP      ORGANIZATION           STATE
vsmart     dtls  55.55.10.3   100.10.1.13   appbee-sdwan-project   up
vbond      dtls  55.55.10.2   100.10.1.12   appbee-sdwan-project   up
vmanage    dtls  55.55.10.1   100.10.1.11   appbee-sdwan-project   up
~~~

✅ vSmart2 has active DTLS relationships with vSmart1, vBond and vManage.

## vBond Orchestrator Connections

Phase 3-relevant rows from show orchestrator connections:

~~~text
PEER TYPE  PROT  SYSTEM IP    PUBLIC IP      ORGANIZATION           STATE
vsmart     dtls  55.55.10.3   100.10.1.13   appbee-sdwan-project   up
vsmart     dtls  55.55.10.4   100.10.1.14   appbee-sdwan-project   up
vmanage    dtls  55.55.10.1   100.10.1.11   appbee-sdwan-project   up
~~~

✅ vBond has active orchestrator relationships with vManage, vSmart1 and vSmart2.

## Phase 3 Validation Summary

| Validation | Result |
|---|---|
| Common organization name | ✅ Passed |
| Root CA chain installed on vManage | ✅ Passed |
| Root CA chain installed on vBond | ✅ Passed |
| Root CA chain installed on vSmart1 | ✅ Passed |
| Root CA chain installed on vSmart2 | ✅ Passed |
| vManage identity certificate valid | ✅ Passed |
| vBond identity certificate valid | ✅ Passed |
| vSmart1 identity certificate valid | ✅ Passed |
| vSmart2 identity certificate valid | ✅ Passed |
| vManage ↔ vBond control relationship | ✅ Passed |
| vManage ↔ vSmart1 control relationship | ✅ Passed |
| vManage ↔ vSmart2 control relationship | ✅ Passed |
| vBond ↔ vSmart1 orchestrator relationship | ✅ Passed |
| vBond ↔ vSmart2 orchestrator relationship | ✅ Passed |
| vSmart1 ↔ vSmart2 control relationship | ✅ Passed |

### Result

**Phase 3 certificate installation, PKI trust establishment and controller onboarding are verified.**
