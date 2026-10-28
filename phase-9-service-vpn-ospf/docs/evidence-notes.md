# Phase 9 Evidence Notes

## Source handling

The Phase 9 working report contains many embedded screenshots. Only screenshots that materially support Phase 9 acceptance are retained as image evidence.

Terminal values that were readable in the report were also transcribed into text under:

`verification/report-transcriptions/`

These text files are explicitly labeled **screenshot transcription** and must not be treated as original raw CLI captures.

## Key evidence chain

1. SITE-PARIS1 joins the Paris service segment and runs OSPF.
2. PRS1 forms OSPF adjacency through CLI configuration.
3. PRS2 forms the equivalent adjacency through vManage templates.
4. Both vEdges learn `192.168.51/52/53.0/24` dynamically through OSPF.
5. SITE-PARIS1 learns remote service routes after OMP redistribution into OSPF.
6. Phase 8 VRRP/DHCP state remains intact.
7. A missing Cyber2-side return path is corrected with explicit routes.
8. Paris-sourced pings toward Cyber2 LAN gateway addresses succeed 5/5.

## Scope boundary

The report also references devices and work that belong to the following BGP phase. Those items are not used as Phase 9 acceptance evidence.

## Superseded test

An earlier unsuccessful end-to-end screenshot was intentionally removed from the repository acceptance evidence after the return-path issue was corrected and a successful test was captured.

The repository therefore presents the final verified state while preserving the troubleshooting cause and corrective configuration through the return-route evidence.
