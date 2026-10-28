# PRS2 DHCP Template Configuration

DHCP Server is configured under the existing Paris VPN 1 LAN interface template.

Values:

- Address Pool: `172.16.51.0/24`
- Exclude:
  - `172.16.51.1`
  - `172.16.51.2`
  - `172.16.51.254`
  - `172.16.51.3`
- Offer Time: `600`
- Lease Time: `86400`
- Admin State: `up`
- Default Gateway: `172.16.51.254`
- DNS Server: `8.8.8.8`

The default gateway deliberately uses the VRRP virtual IP rather than either vEdge's physical address.

Observed DHCP lease on PRS2:

- client IP: `172.16.51.69`
- host name: `Router`
- static binding: `false`
