# VLAN Layout

This document outlines the logical VLAN segmentation plan and how it will be physically implemented across firewall interfaces, switches, and wireless access points.

---

## VLAN Overview

| VLAN ID | Name         | Purpose                  | Subnet           |
|---------|--------------|--------------------------|------------------|
| 10      | Admin        | Workstations, laptops, IT admin tools | 10.10.10.0/24 |
| 20      | Media        | Plex server and other media devices   | 10.20.20.0/24 |
| 30      | IoT          | Smart TVs, streaming sticks, home automation | 10.30.30.0/24 |
| 40      | Guest        | Untrusted guest WiFi traffic         | 10.40.40.0/24 |

---

## Physical Port / Interface Mapping (Planned)

| Device       | Interface | VLANs Tagged      | VLANs Untagged | Notes                          |
|--------------|-----------|-------------------|----------------|--------------------------------|
| Protectli FW | LAN0      | 10,20,30,40       | —              | Trunk port to switch           |
| Switch Port 1|           | 10,20,30,40       | —              | Trunk to access point          |
| Switch Port 2|           | —                 | 10             | Workstation (Admin VLAN)       |
| Switch Port 3|           | —                 | 20             | Plex server                    |
| Switch Port 4|           | —                 | 30             | IoT device hub                 |
| Switch Port 5|           | —                 | 40             | Optional: Guest AP bridge      |

---

## Wireless SSID to VLAN Mapping

| SSID Name      | VLAN ID | Use Case                  |
|----------------|---------|---------------------------|
| `admin-wifi`   | 10      | Trusted work devices      |
| `media-wifi`   | 20      | TV and casting devices    |
| `iot-wifi`     | 30      | Smart home/IoT traffic    |
| `guest-wifi`   | 40      | Internet-only guest use   |

---

## Trunking Plan

- **Firewall → Switch:** All VLANs are tagged and trunked over a single port.
- **Switch → AP:** VLANs are passed to the access point for SSID-to-VLAN mapping.
- **Switch → End Devices:** Ports are untagged per VLAN to isolate traffic.

---

## Notes

- All VLANs will be terminated and routed at the firewall (OPNsense).
- Intra-VLAN routing will be disabled by default.
- Only the Admin VLAN will have full access to management interfaces and configuration portals.
- Inter-VLAN rules will be implemented using strict “default deny” posture, with granular exceptions defined in firewall rules.


