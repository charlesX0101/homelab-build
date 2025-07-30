# VLAN Layout

This document outlines the logical VLAN segmentation plan and how it will be physically implemented across firewall interfaces, switches, and wireless access points.

---

## VLAN Overview

| VLAN ID | Name   | Purpose                                   | Subnet         |
|---------|--------|-------------------------------------------|----------------|
| 10      | Admin  | Workstations, laptops, IT admin tools     | 10.10.10.0/24  |
| 20      | Media  | Plex server and other media devices       | 10.20.20.0/24  |
| 30      | IoT    | Smart TVs, streaming sticks, automation   | 10.30.30.0/24  |
| 40      | Guest  | Untrusted guest WiFi traffic              | 10.40.40.0/24  |

---

## Physical Port and Interface Mapping

| Device        | Interface | VLANs Tagged    | VLANs Untagged | Notes                            |
|---------------|-----------|-----------------|----------------|----------------------------------|
| Protectli FW  | LAN0      | 10,20,30,40     | —              | Trunk port to managed switch     |
| Switch Port 1 |           | 10,20,30,40     | —              | Trunk port to wireless AP        |
| Switch Port 2 |           | —               | 10             | Admin workstation                |
| Switch Port 3 |           | —               | 20             | Plex/media server                |
| Switch Port 4 |           | —               | 30             | IoT hub or controller            |
| Switch Port 5 |           | —               | 40             | Guest AP bridge (optional)       |

---

## Wireless SSID to VLAN Mapping

| SSID Name    | VLAN ID | Purpose                      |
|-------------|---------|------------------------------|
| admin-wifi  | 10      | Trusted laptops and devices  |
| media-wifi  | 20      | Smart TVs, casting devices   |
| iot-wifi    | 30      | IoT and smart home traffic   |
| guest-wifi  | 40      | Internet-only guest devices  |

---

## Trunking Plan

- Firewall to switch uses one trunk port carrying all VLANs tagged.
- Switch to access point uses a tagged trunk link for SSID-VLAN assignment.
- End device ports are untagged and assigned to the appropriate VLAN.
- The firewall routes all VLANs internally but applies strict access rules.

---

## Notes

- All VLAN gateways are configured on OPNsense and centrally routed.
- Admin VLAN is the only segment allowed to access management interfaces.
- Inter-VLAN routing is disabled by default and selectively allowed via firewall rules.
- VLAN tagging is enforced at both the switch and AP levels for Layer 2 segmentation.

