# subnet-planning.md

##Subnet Planning

This document outlines the IP address scheme used in the segmented homelab network. Each VLAN is assigned its own /24 subnet. DHCP scopes, gateway addresses, and reserved static IPs are centrally managed through OPNsense.

All address ranges are non-overlapping. Broadcast domains are isolated. Inter-VLAN routing is blocked by default and allowed only through explicit firewall rules.

---

#VLAN 10 – LAN (Trusted Admin Zone)
Subnet:       10.0.10.0/24
Gateway:      10.0.10.1
DHCP Range:   10.0.10.100 – 10.0.10.199
Static IPs:
  10.0.10.1   OPNsense (LAN interface)
  10.0.10.2   Managed Switch
  10.0.10.10  Admin Workstation
Notes:
  Reserved for core management access, configuration, and firewall GUI.

---

#VLAN 20 – LAB
Subnet:       10.0.20.0/24
Gateway:      10.0.20.1
DHCP Range:   10.0.20.100 – 10.0.20.199
Static IPs:
  10.0.20.10  Plex Media Server
  10.0.20.11  VM Host or Attack Box
Notes:
  Used for security testing, staging environments, VM boxes, and CLI testing.

---

#VLAN 30 – HOME
Subnet:       10.0.30.0/24
Gateway:      10.0.30.1
DHCP Range:   10.0.30.100 – 10.0.30.199
Static IPs:
  10.0.30.10  Work-from-home Desktop
Notes:
  Default segment for personal and daily-use machines.

---

#VLAN 40 – IOT
Subnet:       10.0.40.0/24
Gateway:      10.0.40.1
DHCP Range:   10.0.40.100 – 10.0.40.199
Static IPs:   (none reserved yet)
Notes:
  Smart devices, displays, speakers, thermostats, and cloud-connected appliances.

---

#VLAN 50 – GUEST
Subnet:       10.0.50.0/24
Gateway:      10.0.50.1
DHCP Range:   10.0.50.100 – 10.0.50.199
Static IPs:   (none reserved)
Notes:
  Guest wireless access. Internet only. No access to LAN, LAB, or HOME zones.

---

#VLAN 60 – DMZ
Subnet:       10.0.60.0/24
Gateway:      10.0.60.1
DHCP Range:   10.0.60.100 – 10.0.60.199
Static IPs:
  10.0.60.10  Honeypot Server (planned)
Notes:
  Reserved for exposed services, public nodes, or IDS/monitoring bait.

---

#Subnet Design Notes

- All VLANs use /24 CIDR for simplicity, with room for growth per zone.
- DHCP is handled per VLAN by OPNsense using interface-based scopes.
- Static IPs are manually assigned to critical infrastructure devices only.
- Local DNS overrides are in place to support internal service resolution.
- VLAN-aware switches and APs enforce Layer 2 segmentation.
- No VLAN is allowed to route to another by default. All exceptions must be defined in the firewall ruleset.

