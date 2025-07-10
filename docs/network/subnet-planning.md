# Subnet Planning

This document outlines the IP address scheme for the home network, including the current flat configuration and the planned segmented layout to be implemented in Phase 2.

---

## Current Network (Flat)

- **CIDR:** `192.168.1.0/24`
- **Gateway:** `192.168.1.1` (Flint Router)
- **DHCP Range:** `192.168.1.100 – 192.168.1.199`
- **Static IP Assignments:**
  - Plex Server: `192.168.1.10`
  - Workstation: `192.168.1.11`
  - Flint Admin Interface: `192.168.1.1`

This flat network is sufficient for testing and service validation, but lacks segmentation and policy enforcement between device types.

---

## Planned VLAN Subnet Layout (Phase 2)

| VLAN | Purpose       | Subnet           | Gateway           | DHCP Range            |
|------|---------------|------------------|-------------------|-----------------------|
| 10   | Admin / Trusted Devices | `10.10.10.0/24`  | `10.10.10.1`     | `10.10.10.100–199`    |
| 20   | Media / Plex  | `10.20.20.0/24`  | `10.20.20.1`      | `10.20.20.100–199`    |
| 30   | IoT Devices   | `10.30.30.0/24`  | `10.30.30.1`      | `10.30.30.100–199`    |
| 40   | Guest WiFi    | `10.40.40.0/24`  | `10.40.40.1`      | `10.40.40.100–199`    |

---

## Subnet Strategy

- Each VLAN will have its own `/24` subnet to simplify broadcast domains and ensure address space isolation.
- DHCP will be scoped per VLAN and managed centrally via OPNsense.
- All services (DNS, VPN, etc.) will be routed through the Admin VLAN and firewalled appropriately.
- Inter-VLAN routing will be **disabled by default** and selectively enabled only where needed.

---

## Notes

- VLAN-aware switches and access points will enforce separation at Layer 2.
- Static IPs will be reserved for core infrastructure (e.g., firewall, Plex, workstation).
- External DNS will be overridden by internal resolver to control name resolution visibility across segments.


