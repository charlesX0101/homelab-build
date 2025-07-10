# Firewall Rules

This document outlines the high-level firewall rule strategy for managing traffic between VLANs, controlling service exposure, and protecting core infrastructure in the segmented home lab environment.

The default posture follows a “deny-by-default, allow-by-exception” model.

---

## Global Policy

- **Default inter-VLAN traffic:** Blocked
- **Outbound internet:** Allowed for all VLANs (except where noted)
- **Inbound external traffic:** Blocked by default; opened via port forwarding only when required (e.g., Plex)
- **Admin interface access:** Only accessible from Admin VLAN (VLAN 10)

---

## VLAN-to-VLAN Access Policy

| Source VLAN | Destination VLAN | Allowed? | Purpose                                       |
|-------------|------------------|----------|-----------------------------------------------|
| 10 (Admin)  | Any              | Yes      | Full access for management and diagnostics    |
| 20 (Media)  | 10 (Admin)       | No       | Media should not reach admin interfaces       |
| 20 (Media)  | Internet         | Yes      | Plex can reach external services              |
| 30 (IoT)    | 20 (Media)       | No       | Prevent IoT access to media hosts             |
| 30 (IoT)    | Internet         | Yes      | Allow updates and cloud integration           |
| 40 (Guest)  | Any Internal     | No       | Guest WiFi is fully isolated                  |
| 40 (Guest)  | Internet         | Yes      | General browsing access only                  |

---

## Service Port Access

### Plex Media Server
- VLAN: 20 (Media)
- Allowed inbound ports:
  - TCP 32400 (from Internet, if port-forwarded)
  - Local access: Only from VLAN 10 (Admin) and VLAN 20 itself

### OPNsense Web UI
- VLAN: 10 (Admin)
- Port: TCP 443 (custom port if obfuscation preferred)
- Blocked from all other VLANs

### DNS / DHCP
- Provided centrally by OPNsense or DNS server in VLAN 10
- DNS allowed from all VLANs outbound to specified resolver
- DNS traffic between VLANs blocked unless explicitly required

### NTP
- Allowed outbound from all VLANs

---

## Logging and Alerting

- All blocked inter-VLAN traffic is logged
- Alerts generated for any unexpected traffic attempts toward Admin VLAN
- Port scans or high-frequency hits from IoT/Guest VLANs trigger alerts

---

## Notes

- Rules are implemented and enforced in OPNsense using interface groups and tagged VLAN interfaces.
- Future service zones (e.g., dev, DMZ) will be assigned separate VLANs and isolated under this same model.
- The firewall ruleset is managed as code (via backup config) and stored securely offline for recovery.


