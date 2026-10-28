# Phase 3 — Controller Certificate Workflow

This document records the certificate workflow used to establish trust between the SD-WAN controllers.

## 1. Root CA Setup

The public CA configuration is stored in:

[../configs/root-ca.cfg](../configs/root-ca.cfg)

Core CA settings:

~~~text
hostname IOS-Root-CA
crypto key generate rsa label PKI modulus 2048

crypto pki server PKI
 database url flash:
 database level complete
 issuer-name cn=rootca.lab.local
 hash sha256
 grant auto
 no shutdown
~~~

The root certificate is exported and made available through TFTP:

~~~text
crypto pki export PKI pem url flash:
tftp-server flash:PKI.ca
~~~

## 2. Install the Root Certificate on a Controller

Primary method:

~~~text
request download tftp://100.10.1.100/PKI.ca
request root-cert-chain install home/admin/PKI.ca
~~~

Documented fallback when the direct download method is unavailable:

~~~text
vshell
tftp -g -r PKI.ca 100.10.1.100
~~~

Then return to the Viptela CLI and install the root chain.

## 3. vManage Identity Certificate

After the root certificate is installed:

1. Open **Administration > Settings**.
2. Configure the SD-WAN organization and vBond information.
3. Set controller certificate authorization to **Enterprise Root Certificate**.
4. Add the enterprise root certificate.
5. Open **Configuration > Certificate > Controllers**.
6. Generate the vManage CSR.
7. Copy the CSR to the Root CA.
8. Sign the CSR:

~~~text
IOS-Root-CA# crypto pki server PKI request pkcs10 terminal
~~~

9. Copy the granted certificate back to vManage.
10. Use **Install Certificate** and verify the installed state.

## 4. vBond Identity Certificate

Add vBond from:

~~~text
Configuration > Device > Controller > Add Controller
~~~

After the root chain is installed on vBond:

1. Generate/view the vBond CSR from vManage.
2. Copy the CSR to the Root CA.
3. Sign it:

~~~text
IOS-Root-CA# crypto pki server PKI request pkcs10 pem terminal
~~~

4. Copy the granted certificate.
5. Install it from the vManage certificate workflow.
6. Verify vBond is onboarded.

## 5. vSmart1 and vSmart2 Identity Certificates

The same workflow is repeated independently for vSmart1 and vSmart2:

1. Add the vSmart controller in vManage.
2. Install PKI.ca on the controller.
3. Generate and view the CSR.
4. Sign the CSR on the Root CA:

~~~text
IOS-Root-CA# crypto pki server PKI request pkcs10 pem terminal
~~~

5. Install the granted certificate.
6. Confirm the controller is synchronized/onboarded.

## 6. Verify Certificate State

On each controller:

~~~text
show control local-properties
~~~

Relevant fields:

~~~text
root-ca-chain-status    Installed
certificate-status      Installed
certificate-validity    Valid
organization-name       appbee-sdwan-project
~~~

## 7. Verify Controller Relationships

vManage:

~~~text
show control connections
~~~

vSmart1 / vSmart2:

~~~text
show control connections
~~~

vBond:

~~~text
show orchestrator connections
~~~

The Phase 3 acceptance condition is that vManage, vBond, vSmart1 and vSmart2 have the expected controller relationships in the up state.

## Public Repository Hygiene

Private keys, password hashes, CA archive passwords and authentication credentials are not stored in this repository.
