# Homelab Project Roadmap

This document outlines the progression of the homelab project across multiple phases. Each phase builds toward a segmented, secure, and service-capable network with enterprise-style architecture.

---

## Project Phases

### Phase 1 – Establish Control (Complete)
- Replace ISP-provided modem/router combo
- Deploy bridge-only cable modem (ARRIS S34)
- Install GL.iNet Flint router with OpenWrt-based firmware
- Establish clean LAN with static IPs
- Deploy first internal service (Plex Media Server)

### Phase 2 – Network Segmentation (In Progress)
- Install and configure Protectli mini PC with OPNsense
- Design VLANs for Admin, Media, IoT, and Guest zones
- Trunk VLANs through managed switch and access point
- Enforce inter-VLAN firewall rules
- Harden access to all admin interfaces

### Phase 3 – Core Services Expansion (Planned)
- Deploy WireGuard VPN for secure remote access
- Set up internal DNS override and static host resolution
- Implement service health monitoring and log aggregation
- Deploy observability stack (e.g., Netdata, Uptime Kuma)

### Phase 4 – Infrastructure as Practice (Planned)
- Treat firewall configuration as version-controlled infrastructure
- Document all network and policy changes
- Test upgrades and rule changes in a separate staging environment
- Maintain secure and encrypted backups for all configs

---

## Current Status

- Phase 1 hardware deployed and operational
- Plex Media Server running on flat network
- Network diagrams and initial documentation completed
- Placeholder subnet and VLAN design completed
- OPNsense testing and hardening underway on a local mini PC
- Documentation structure and content finalized

---

## Upcoming Milestones

- Finalize Protectli hardware selection
- Deploy OPNsense in passive (monitor-only) mode on LAN
- Replace Flint as primary router with OPNsense
- Integrate managed switch and apply VLAN trunking
- Isolate Plex server into dedicated Media VLAN
- Implement inter-VLAN firewall policy
- Enable WireGuard VPN access for remote administration
- Establish internal DNS service with static host records

---

## Stretch Goals

- Add reverse proxy for internal domain-based routing
- Build automated encrypted backup routine
- Implement multi-SSID VLAN mapping via access points
- Centralize logs to syslog/monitoring node
- Explore port-based access control or MAC filtering
- Publish externally viewable portfolio or documentation site

---

## Change Log

This section will track major configuration or architectural changes as they are implemented across the project lifecycle.


