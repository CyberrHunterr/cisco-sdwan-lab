# Lessons Learned — Phase 2

- Keep System IP, transport IP and management IP conceptually separate.
- Use VPN 0 for transport-side controller connectivity.
- Use VPN 512 for management connectivity.
- Verify base IP reachability before troubleshooting certificates or onboarding.
- Keep redundant vSmart instances documented independently.
- Do not publish password hashes or authentication secrets in a public repository.
- When the live lab has progressed beyond the documented phase, state clearly which evidence is historical and which is current.
