# opnsense-hardening.md

#OPNsense Hardening Strategy

This document outlines the hardening measures applied to the live OPNsense
firewall deployment running on a Protectli FW6E appliance. These controls are
designed to minimize attack surface, enforce strict administrative access, and
ensure that all exposed services are intentional, auditable, and limited.

------------------------------------------------------------

#Access Control

WebUI Access:
- Restricted to VLAN 10 (Admin)
- Explicitly blocked on all other interfaces including WAN

Custom Ports:
- Web UI port changed from TCP 443 to a non-standard port
- SSH service (if enabled) moved off port 22

SSH Lockdown:
- SSH is disabled by default
- If enabled, access is restricted to known internal clients
- Password authentication is disabled
- Key-based login is required

User Management:
- Only a single admin account is present
- Default admin credentials changed
- No shell access granted to non-admin users

------------------------------------------------------------

#WAN and Service Exposure

VPN Access:
- WireGuard is the only service exposed on the WAN interface
- WAN rules allow only the specific UDP VPN port
- Connection attempts are logged and rate-limited

Port Forwarding:
- TCP 32400 is optionally open for Plex media access
- Forwarded only to the Plex host on VLAN 20
- No other inbound ports are exposed by default

Bogon and Private Blocks:
- Bogon networks blocked on WAN
- Private ranges also blocked on WAN

Anti-Lockout Rule:
- Disabled
- Admin access explicitly defined and limited to VLAN 10

------------------------------------------------------------

#Interface Behavior and Segmentation

- Each VLAN interface is assigned its own firewall ruleset
- Inter-VLAN access is denied by default
- Admin interface is not accessible from any non-admin segment
- Static mappings are defined for all core devices including switch, AP,
  workstation, and Plex server

------------------------------------------------------------

#DNS and DHCP Enforcement

- DNS rebinding protection enabled
- Resolver limited to upstream providers (e.g. Quad9, Cloudflare)
- DNS traffic is allowed only to the internal resolver
- DHCP leases restricted to known interfaces
- Static reservations are configured for all infrastructure devices

------------------------------------------------------------

#Logging and Monitoring

- Logs retained for all:
  - Blocked inter-VLAN traffic
  - VPN handshakes
  - Port forward hits
  - Web UI access attempts
- Firewall is being integrated with local monitoring (Uptime Kuma)
- Optional syslog forwarding under consideration

------------------------------------------------------------

#Advanced Features (Staged or Under Evaluation)

- Zenarmor and Suricata being evaluated for inline traffic inspection
- DNSBL or Pi-hole integration under review for ad and tracker blocking
- DoH and DoT upstream resolution support under consideration

------------------------------------------------------------

#Backups and Recovery

- Full configuration backups exported after each rule or interface change
- Backup files are stored offline and versioned manually
- No auto-sync or cloud exposure of firewall configuration
- Recovery device and fallback config prepared for emergency redeployment

------------------------------------------------------------

#Patch Management

- Auto-updates disabled
- Firmware updates reviewed and tested before installation
- Test changes and package upgrades trialed in a separate lab image
- Product

