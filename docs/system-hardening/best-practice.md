# Homelab Best Practices

This document outlines general best practices applied throughout the homelab to improve operational security, maintainability, and long-term scalability. These practices are followed across all systems and devices, from the firewall to internal service nodes.

---

## Access & Authentication

- Disable default usernames wherever possible
- Enforce key-based SSH authentication; disable password login
- Use strong local passwords and store securely offline
- Limit admin-level access to a single user per system
- Restrict management interfaces (web, SSH) to VLAN 10 only

---

## Segmentation & Surface Area Reduction

- Apply the principle of least privilege to VLAN-to-VLAN access
- Default deny all inter-VLAN traffic unless explicitly needed
- Avoid “allow all” rules for diagnostics or convenience
- Never expose management ports directly to WAN
- Separate IoT, guests, media, and admin traffic via VLANs

---

## DNS & IP Control

- All core devices use static IPs
- DNS rebinding protection is enforced
- Internal DNS resolver configured with local host overrides
- External DNS access restricted to trusted resolvers (e.g., Quad9, Cloudflare)

---

## Software & Firmware

- Disable auto-updates on all infrastructure
- Apply updates only after reading changelogs and verifying impact
- Perform test updates in a mock environment first when possible
- Keep offline backups of current working configurations

---

## Backups

- Maintain encrypted, versioned backups of:
  - Firewall configs
  - Router settings
  - DHCP/DNS reservations
  - Static mappings and IP plans
- Store at least one backup copy offline and off-network

---

## Monitoring & Alerting

- Log firewall denials, VPN handshakes, and WAN activity
- Monitor uptime and health with lightweight internal tools (e.g., Uptime Kuma)
- Periodically review logs for unexpected behavior
- Track open ports and run internal port scans to audit exposure

---

## Service Hosting

- Only expose services that are necessary
- Prefer internal reverse proxies with TLS for internal service access
- Keep externally accessible services (e.g., Plex) isolated by VLAN and firewall scope
- Use host-based firewalls in addition to network-level segmentation when applicable

---

## Operational Discipline

- Document all changes to the network stack, even small ones
- Commit rule changes and major config edits to version-controlled notes
- Use staging/test environments for anything that affects the firewall or routing core
- Assume that convenience shortcuts create long-term maintenance debt

---

## Culture of Ownership

This lab is built for deliberate control — not automation-first, not convenience-first. Every rule, device, and port exists for a reason, and every service earns its exposure.

Security is not an overlay — it's the foundation.

