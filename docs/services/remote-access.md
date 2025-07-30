# remote-access.md

#Remote Access

This document outlines how remote access to the homelab is configured and
controlled. It includes VPN access policy, SSH exposure rules, and overall
external management constraints. Remote access is tightly limited and designed
to avoid exposing any direct administrative interfaces to the public internet.

------------------------------------------------------------

#Remote Access Objectives

- Allow secure remote management of firewall, internal hosts, and services
- Avoid exposing the firewall UI or switch/AP interfaces to WAN traffic
- Support controlled VPN access from trusted clients only
- Log and monitor all inbound connections and authentication attempts
- Ensure recovery is possible even in the event of on-site failure

------------------------------------------------------------

#WireGuard VPN

Status: Configured or ready for deployment on OPNsense

Role: Primary secure tunnel for remote access
Location: Hosted on OPNsense (VLAN 10)
Protocol: UDP (custom port)
Authentication: Key-based only (no password or shared secret)

Client Access Scope:
- Full access to VLAN 10 (Admin) for GUI, SSH, and backups
- Optional access to VLAN 20 (LAB) or VLAN 30 (HOME) depending on role
- No access to VLANs 40 (IOT), 50 (GUEST), or 60 (DMZ)

Notes:
- Tunnel logs are retained and monitored for unusual patterns
- Firewall pinhole allows VPN handshake only from trusted external IPs
- Future plan includes TOTP or MFA for session initiation

------------------------------------------------------------

#SSH Access

- SSH is restricted to VLAN 10 (Admin) only
- No SSH access from WAN, Guest, or IOT zones
- VPN clients may SSH into core systems only if explicitly allowed

Hardening Controls:
- SSH key-based authentication only
- Port obfuscation (non-standard port)
- Fail2ban or similar lockout enforcement for brute-force attempts
- All SSH logins and failures are logged centrally

------------------------------------------------------------

#WAN Exposure Policy

- No direct WAN access to firewall or switch interfaces
- No service ports are exposed to the internet except Plex (optional)
- All external management must flow through WireGuard tunnel

DNS and Tunneling:
- DNS resolution is blocked from untrusted sources
- DNS tunneling and split tunneling are blocked at the firewall

------------------------------------------------------------

#Monitoring and Logging

- VPN and SSH logs are collected on OPNsense and reviewed periodically
- Unusual activity triggers local alerts or syslog forwarding
- Future monitoring will include:
  - Uptime Kuma for tunnel state
  - Netdata or equivalent for bandwidth and endpoint monitoring
  - Optional webhook or email alerts for login activity

------------------------------------------------------------

#Recovery and Failsafe Plan

- A dedicated laptop is preconfigured with VPN keys and stored offline
- VPN configuration backups are stored securely off-device
- Firewall rulesets are versioned and backed up for fast redeployment
- A printed recovery plan is stored alongside encrypted digital copies

