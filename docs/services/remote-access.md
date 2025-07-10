# Remote Access

This document outlines how remote access to the homelab is planned and controlled, including VPN configuration, SSH access policies, and restrictions for secure administration.

---

## Remote Access Goals

- **Allow secure remote management** of the firewall, services, and internal hosts
- **Avoid exposing any admin interfaces** directly to the public internet
- **Support outbound access into the homelab for testing and maintenance**
- **Log and monitor all inbound access attempts**

---

## Phase 1 (Current)

- **No active remote access enabled**
- Management is performed locally over the LAN
- Plex server is optionally exposed via port forwarding (TCP 32400)
  - External access is limited to known client devices
  - Firewall monitors port usage and alerts on anomalies

---

## Phase 2 (Planned)

### WireGuard VPN

- **Role:** Primary secure tunnel for remote access into the homelab
- **Location:** Hosted on OPNsense (VLAN 10)
- **Port:** UDP (custom port)
- **Authentication:** Key-based (no password or shared secrets)
- **Client Access Scope:**
  - Full access to Admin VLAN (10)
  - Limited access to other VLANs depending on client role
- **Use Case:** Admin access to internal web UIs, SSH endpoints, and dashboards

### SSH Access

- **Allowed From:** Admin VLAN only
- **Exposed To:** VPN clients (not WAN)
- **Hardened With:**
  - Key-based login only
  - Port obfuscation (non-22)
  - Fail2ban-style lockout for brute-force attempts

---

## External Management Boundaries

- **No direct WAN access** to OPNsense, router, or service ports (besides Plex, optionally)
- All remote access is required to flow through WireGuard or manually defined SSH relay points
- DNS access is restricted per VLAN; DNS tunneling is blocked at firewall level

---

## Monitoring and Auditing

- All remote connections (VPN, SSH) are logged centrally
- Admin VLAN will run Uptime Kuma or equivalent to alert on tunnel downtime
- Future plan includes multi-factor auth for VPN initiation (e.g., TOTP + key)

---

## Failover / Recovery Strategy

- A dedicated management laptop with preconfigured VPN keys will be stored offline for recovery scenarios
- Backup VPN configs and firewall rules will be versioned and stored in a separate secure repo or physical backup


