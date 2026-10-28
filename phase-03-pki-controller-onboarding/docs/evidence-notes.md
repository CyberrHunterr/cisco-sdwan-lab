# Phase 3 Evidence Notes

## Evidence Used

Phase 3 is documented from:

- the Phase 3 implementation workflow,
- the sanitized Root CA configuration,
- current live CLI state from vManage,
- current live CLI state from vBond,
- current live CLI state from vSmart1,
- current live CLI state from vSmart2.

## Certificate State

Current live controller output confirms the enterprise trust chain and controller identity certificates remain installed.

| Controller | Root CA Chain | Certificate Status | Certificate Validity |
|---|---|---|---|
| vManage | Installed | Installed | Valid |
| vBond | Installed | Installed | Valid |
| vSmart1 | Installed | Installed | Valid |
| vSmart2 | Installed | Installed | Valid |

The current organization name is consistent across all four controllers:

~~~text
appbee-sdwan-project
~~~

## Root Certificate Details

The vBond certificate store exposes the enterprise Root CA certificate with:

~~~text
Issuer:  CN=rootca.lab.local
Subject: CN=rootca.lab.local
Signature Algorithm: sha256WithRSAEncryption
RSA Public-Key: 2048 bit
CA:TRUE
~~~

The Root CA certificate validity observed on vBond is:

~~~text
Not Before: Aug 11 19:28:20 2026 GMT
Not After : Aug 10 19:28:20 2029 GMT
~~~

## Controller Verification Scope

The live lab has advanced beyond Phase 3 and currently includes vEdge sessions.

Those vEdge rows are intentionally excluded from Phase 3 validation.

Only these controller relationships are used as Phase 3 evidence:

- vManage ↔ vBond
- vManage ↔ vSmart1
- vManage ↔ vSmart2
- vBond ↔ vSmart1
- vBond ↔ vSmart2
- vSmart1 ↔ vSmart2

## Sanitization

The public repository does not include:

- private keys,
- password hashes,
- plaintext controller credentials,
- CA archive passwords,
- raw certificate private material.

Only configuration required to explain the PKI design and non-sensitive verification output is retained.
