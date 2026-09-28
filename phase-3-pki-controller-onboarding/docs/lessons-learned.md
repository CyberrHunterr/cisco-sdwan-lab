# Phase 3 — Lessons Learned

## Reachability and Trust Are Different Layers

Phase 2 proved that the controllers could reach one another at the IP layer.

Phase 3 showed that IP reachability alone is not sufficient for the SD-WAN control plane. The controllers also require trusted identity certificates before authenticated control relationships can be established.

## A Common Root CA Simplifies Trust

Instead of configuring every controller to directly trust every other controller certificate, the lab uses a shared Root CA.

Once each controller trusts the same CA, certificates signed by that CA can participate in the common trust model.

## Organization Identity Must Be Consistent

The live controllers use:

~~~text
appbee-sdwan-project
~~~

as the common organization name.

Certificate and controller identity workflows depend on consistency across the fabric. Small mismatches in identity-related values can prevent onboarding even when network reachability is correct.

## Certificate Onboarding Is a Dependency Chain

The workflow is sequential:

~~~text
Root CA
  ↓
Root certificate distribution
  ↓
CSR generation
  ↓
CSR signing
  ↓
Identity certificate installation
  ↓
Control-plane verification
~~~

A problem early in the chain blocks later controller onboarding.

## GUI and CLI Evidence Complement Each Other

vManage provides the controller certificate workflow and inventory view, while CLI commands expose the actual installed certificate and control-connection state.

Useful verification commands include:

~~~text
show control local-properties
show control connections
show orchestrator connections
show certificate root-ca-cert
~~~

## Current-State Output Must Be Filtered by Phase

The lab continued into later phases, so current controller outputs contain vEdge sessions that did not belong to Phase 3.

For a clean engineering record, Phase 3 evidence must isolate controller-to-controller relationships rather than treating the complete present-day output as historical Phase 3 state.

## Public PKI Documentation Requires Sanitization

Certificate architecture can be documented without publishing secrets.

The repository intentionally excludes private keys, password hashes, CA archive passwords and authentication credentials while retaining enough configuration to reproduce the design.
