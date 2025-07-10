# OPNsense / pfSense Hardening Plan

This document outlines the firewall hardening strategy for the future production OPNsense deployment. These steps are being actively tested and refined on a local mini PC mockup to validate the process and configuration before rollout to the primary homelab firewall (Protectli appliance).

The hardening plan focuses on controlling administrative access, limiting surface area, and ensuring all service exposure is intentional and auditable.

---

## Active Testing Environment

A local mini PC has been set up with a mock OPNsense install to practice:

- Admin interface lockdown
- Firewall rule development
- VPN and SSH secure access setup
- Logging, DNS override, and interface isolation

This sandbox environment allows the entire firewall build to be stress-tested and versioned before live deployment.

---

## Access Control

- **WebUI Restriction:**
  - Accessible only from Admin VLAN (VLAN 10)
  - Blocked on WAN and non-admin interfaces

- **Custom Ports:**
  - WebUI port changed from `443` to an uncommon port
  - SSH moved off port `22`

- **SSH Lockdown:**
  - Password login disabled
  - Key-based access only from known clients
  - SSH disabled entirely unless actively needed

- **User Management:**
  - Only one non-default admin account
  - No unnecessary shell users

---

## WAN & Service Exposure

- **VPN (WireGuard):**
  - Only port exposed on WAN interface
  - Connection attempts logged and rate-limited

- **Plex Port Forwarding (Optional):**
  - TCP 32400 allowed only to internal media server (VLAN 20)
  - All other inbound access is disabled by default

---

## Interface Settings

- Block private and bogon networks on WAN
- Anti-lockout rule disabled in favor of explicit admin rules
- Static mappings for all core devices (router, Plex, workstation)

---

## DNS & DHCP Controls

- DNS rebinding protection enabled
- Only approved upstream resolvers allowed (e.g. Quad9, Cloudflare)
- DHCP reservations for infrastructure devices to ensure consistent IPs

---

## Logging & Monitoring

- Log all inter-VLAN traffic denials
- Log VPN handshakes, port forwards, and WAN hits
- Testing integration with Uptime Kuma and optional remote syslog in mockup

---

## Advanced Features (Under Evaluation)

- Zenarmor or Suricata for intrusion detection
- DNSBL or Pi-hole integration for ad/tracker blocking
- Enforced DoH/DoT upstream resolution

---

## Backups & Recovery

- Configuration backups exported regularly from the test box
- Backup stored offline and synced manually after any rule or firmware change
- Final deployment will follow same backup policy

---

## Patch Management

- Firmware updates reviewed before install
- Auto-updates disabled
- Practice updates applied to the mockup first before pushing to production system

---

## Summary

The goal is to reduce exposure, isolate control surfaces, and keep every open port deliberate. The mock environment ensures that mistakes, regressions, or lockouts are handled in testing — not in production.


