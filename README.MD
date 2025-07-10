# homelab-build

Documentation-first blueprint for transitioning from locked-down ISP gear to a segmented, enterprise-grade home network.

## Purpose

This project documents the real-world process of rebuilding a home network from the ground up using consumer-accessible hardware and open-source tools.

It is designed for those who want full ownership and control over their network — for cybersecurity learning, homelab services, and remote work infrastructure — without relying on restrictive ISP-provided equipment.

## Background

The original setup used a Technicolor CGM4140COM “Panoramic WiFi Gateway” supplied and configured by the ISP. This all-in-one modem/router offered no VLAN support, limited administrative access, and lacked the flexibility needed for secure segmentation or advanced routing.

To move toward a more professional and manageable network, this setup was decommissioned in favor of a modular, user-owned solution.

## Current Build (Phase 1)

The current foundation is a clean, user-controlled LAN with modern hardware and no vendor lock-in:

- **Cable Modem:** ARRIS S34 DOCSIS 3.1 (bridge-only modem)
- **Router:** GL.iNet Flint AX1800 (WiFi 6) with full admin access
- **Firmware:** OpenWrt-based UI with control over DHCP, DNS, routing, and basic firewall rules
- **Services:** Self-hosted Plex Media Server running on the flat network

This configuration represents Phase 1 of the rebuild. It reclaims full control from the ISP and establishes a secure, flexible base for further upgrades.

## Planned Upgrade (Phase 2)

The next step is a full migration to segmented, enterprise-style networking:

- Deploy a Protectli mini PC running OPNsense as the core firewall and router
- Implement VLAN segmentation across physical and virtual zones:
  - VLAN 10: Admin / Workstations
  - VLAN 20: Media / Plex Server
  - VLAN 30: IoT Devices
  - VLAN 40: Guests
- Define strict inter-VLAN firewall rules to isolate services and reduce attack surface
- Introduce IDS/IPS, site-to-site VPN, and secure remote access
- Explore remote media access, external backup routines, and uptime monitoring

Phase 2 is in progress and will be documented in detail as upgrades are implemented.

## Documentation Map

Documentation and diagrams are organized in the `/docs` and `/diagrams` directories:

- `docs/introduction.md` – project background and purpose
- `docs/hardware/` – bill of materials, device roles
- `docs/network/` – subnet planning,

