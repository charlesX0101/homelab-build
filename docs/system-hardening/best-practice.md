# best-practices.md

#Homelab Best Practices

This document outlines general best practices applied throughout the homelab to
improve operational security, maintainability, and long-term scalability. These
principles are followed consistently across all systems and infrastructure
components, from the firewall to internal service nodes.

------------------------------------------------------------

#Access and Authentication

- Default usernames are disabled or removed wherever possible
- SSH access uses key-based authentication only
- Password login is disabled on all devices that support it
- Strong local admin passwords are used and stored securely offline
- All management interfaces (web, SSH, VPN) are restricted to VLAN 10
- No administrative interfaces are reachable from the WAN

------------------------------------------------------------

#Segmentation and Surface Area Reduction

- VLANs are designed with least-privilege in mind
- All inter-VLAN traffic is denied by default
- Exceptions are tightly scoped and logged
- Diagnostic shortcuts and "allow all" rules are avoided
- IoT, guest, lab, and admin traffic are strictly separated at Layer 2
- No VLAN has routing visibility unless explicitly required

------------------------------------------------------------

#DNS and IP Control

- All infrastructure devices use static IPs with defined reservations
- Local DNS is resolved via OPNsense with hostname overrides
- DNS rebinding protection is enforced at the resolver level
- DNS requests are allowed only to internal resolver or trusted upstreams
- External DNS resolution is limited to providers like Quad9 or Cloudflare

------------------------------------------------------------

#Software and Firmware

- Auto-updates are disabled on all infrastructure systems
- Updates are applied only after changelogs are reviewed
- When possible, updates are tested on a staging system before production
- Configuration snapshots are taken before any firmware or package change
- All updates are documented with version and timestamp

------------------------------------------------------------

#Backups

- Backups are encrypted, versioned, and stored in multiple locations
- At minimum, the following are backed up:
  - OPNsense configuration exports
  - Static DHCP and DNS mappings
  - VLAN schema and port layout
  - IP planning notes and interface design
- One full backup is always stored offline and off-network

------------------------------------------------------------

#Monitoring and Alerting

- All denied firewall traffic is logged
- VPN connection events are recorded and reviewed
- WAN interface hits are logged and alert thresholds are defined
- Internal tools like Uptime Kuma or Netdata are used to track service uptime
- Periodic internal port scans are performed to detect accidental exposure

------------------------------------------------------------

#Service Hosting

- Only essential services are exposed internally or externally
- Reverse proxies are preferred for internal web access (planned)
- TLS is used for internal dashboard access wherever possible
- Host-based firewalls are used on service nodes when supported
- Externally reachable services (e.g., Plex) are fully isolated by VLAN

------------------------------------------------------------

#Operational Discipline

- All network changes are documented immediately
- Firewall rules and switch configurations are version-controlled as text
- All major changes are tested on a separate system when possible
- No undocumented rules or exceptions are permitted
- Convenience shortcuts are considered maintenance debt

------------------------------------------------------------

#Culture of Ownership

This lab is built for deliberate control. It is not optimized for automation,
and not driven by convenience. Every port, rule, and device is present for a
reason. Every interface is intentional. Security is not an optional layer; it is
the foundation of this design.


