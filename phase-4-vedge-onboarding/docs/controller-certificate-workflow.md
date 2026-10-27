# Controller Certificate Workflow

## 1. Install the Root CA

The vEdge first downloads the Root CA certificate and installs it into the local trust chain.

Typical workflow:

```text
request download tftp://100.10.1.100/PKI.ca
```

If direct download is unavailable:

```text
vshell
tftp -g -r PKI.ca 100.10.1.100
```

Then:

```text
request root-cert-chain install home/admin/PKI.ca
```

## 2. Generate the CSR

```text
request csr upload home/admin/csr.txt
```

The organization unit must match the SD-WAN organization name:

```text
appbee-sdwan-project
```

## 3. Sign and install the device certificate

The CSR is signed by the IOS Root CA. The signed certificate is then installed on the vEdge:

```text
request certificate install home/admin/cert.txt
```

Private keys, CSR bodies and granted-certificate bodies are not stored in this public repository.

## 4. Register chassis and serial identity

After certificate installation, the vEdge exposes its chassis/serial identity:

```text
show certificate serial
```

The identity is added to vManage and vBond and distributed to the controllers.

## 5. Verify onboarding

Final checks include:

```text
show control local-properties
show certificate serial
show certificate root-ca-cert
show certificate installed
show control connections
```

On vSmart:

```text
show omp peers
show control connections
```
