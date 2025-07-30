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
- Deploy observability stack (e.g. Netdata, Uptime Kuma)

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
- VLAN and subnet design finalized
- OPNsense testing and hardening underway on a local mini PC
- GitHub documentation and config structure established

---

## Upcoming Milestones

- Finalize Protectli firewall deployment with VLAN trunking
- Promote OPNsense to primary router and migrate LAN duties
- Isolate media services into dedicated Media VLAN
- Enforce finalized inter-VLAN firewall ruleset
- Enable WireGuard VPN for secure remote administration
- Stand up internal DNS override via OPNsense or Pi-hole
- Begin segmented testing of log aggregation and monitoring stack

---

## Stretch Goals

- Add reverse proxy for internal domain-based service routing
- Implement automated encrypted backup pipeline for configs
- Integrate UniFi AP with full SSID-to-VLAN mapping
- Centralize logs with syslog-compatible agent or Netdata
- Evaluate MAC filtering or per-port auth for lab hardware
- Publish externally viewable portfolio or documentation site

---

## "From the Lab" – Upcoming Project Repositories

To accompany this roadmap, individual repositories will be created for each core setup. These deep-dive walkthroughs will document the build process and showcase skills for portfolio and operational use.

Planned repo topics include:

- monitoring-box – Setup of mini PC running Netdata and Suricata for hybrid SIEM and observability
- media-server – Full deployment of Plex on a secure VLAN with optional remote access
- file-server – NAS and PXE boot server with backup routines and test image deployment
- pi-core – Raspberry Pi hosting Pi-hole and optionally Gitea for internal Git repositories
- proxmox-lab – Standalone Proxmox host for virtualized homelab environments

These labs will follow a consistent format with README.md, configuration files, screenshots, and optionally shell scripts to support reproducibility.

---

## Change Log

Coming soon – will begin tracking once Phase 2 is finalized

