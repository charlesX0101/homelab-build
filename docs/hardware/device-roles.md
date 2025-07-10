# Device Roles

This document describes the functional role of each key component in the homelab network, with focus on how control, segmentation, and future upgrades are shaped by device capabilities.

---

## ARRIS S34 DOCSIS 3.1 (Cable Modem)

- **Role:** Pure modem — provides a clean, bridged connection to the ISP.
- **Reasoning:** This device removes all NAT, routing, and WiFi responsibilities from the modem layer, allowing full control to shift to the router.
- **Benefits:**
  - No double NAT
  - No ISP lock-in
  - Transparent handoff to user-managed router

---

## GL.iNet Flint AX1800 (Router + WiFi AP)

- **Role:** Primary LAN gateway and WiFi access point
- **Capabilities:**
  - DHCP, DNS, basic firewall
  - WiFi 6 for modern wireless clients
  - OpenWrt-based firmware for advanced customization
- **Current Tasks:**
  - Handles all internal routing
  - Hosts port-forwarding and static leases for internal services
- **Limitations:**
  - Lacks VLAN support across interfaces
  - Not ideal for inter-VLAN firewall rules or intrusion detection
  - Will eventually be demoted to access point role only

---

## Plex Media Server

- **Role:** Internal service host and media platform
- **Network Position:** Static IP on the flat LAN
- **Use Case:**
  - Early proof-of-concept for internal service hosting
  - Used to validate port forwarding, internal DNS, and throughput under load
- **Planned Migration:**
  - Will be moved to a dedicated VLAN in Phase 2
  - Access limited by firewall rules (e.g., only accessible by trusted devices)

---

## Workstation (Admin Node)

- **Role:** Primary configuration and monitoring machine
- **Functions:**
  - Used to log into router/firewall interfaces
  - Hosts configuration backups and planning files
  - May later host lightweight observability tools (Uptime Kuma, Netdata)

---

## Mobile Devices, Smart TV, etc.

- **Role:** Network clients used to test normal traffic flows
- **Current Setup:**
  - All reside on same LAN (Phase 1)
- **Planned Change:**
  - Mobile/work devices will move to a trusted VLAN
  - Media clients (TV, streamers) will shift to an isolated segment

---

## Future Devices

### Protectli Mini PC (Planned Core Firewall)

- **Planned Role:** Core gateway, router, and firewall for the entire network
- **To Run:** OPNsense
- **Responsibilities:**
  - VLAN trunking
  - Inter-VLAN firewall enforcement
  - IDS/IPS services
  - WireGuard/OpenVPN access
  - DHCP relay and DNS overrides

### Managed Switch (Planned)

- **Planned Role:** VLAN-aware Layer 2 switching
- **Purpose:**
  - Enforce port-based segmentation
  - Trunk VLANs to access points and service nodes

### Dedicated AP (Planned)

- **Planned Role:** VLAN-aware wireless access point
- **Use Case:**
  - Separate SSIDs tied to different VLANs (e.g., Work, Guest, IoT)
  - Handled through trunk port from switch


