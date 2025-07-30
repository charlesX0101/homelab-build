# device_roles.md

#Device Roles

This document describes the role of each core component in the segmented homelab
network. It explains how control is enforced, how traffic is segmented, and how
each device contributes to a secure, modular infrastructure.

------------------------------------------------------------

#ARRIS S34 DOCSIS 3.1 (Cable Modem)
Role: Pure modem
Notes: Transparent bridge to ISP. No routing, NAT, or WiFi functions.

------------------------------------------------------------

#Protectli Vault FW6E (Firewall and Router)
Role: Core gateway and segmentation point
Notes:
- Runs OPNsense
- Manages VLANs, DHCP, DNS, firewall rules
- Provides trunked VLAN interface to switch
- Optional future use: Suricata IDS/IPS, VPN server

------------------------------------------------------------

#TP-Link TL-SG2210MP (Managed Switch)
Role: VLAN trunking and access port isolation
Notes:
- Tagged trunk uplink to Protectli firewall
- Tagged downlink to UniFi AP
- Untagged access ports mapped per VLAN
- Provides PoE to access point

------------------------------------------------------------

#TP-Link TL-SG1210MP (Unmanaged Switch)
Role: Expansion switch for LAB VLAN
Notes:
- Connected to access port carrying untagged VLAN 20
- Used for wired test systems, attack boxes, or isolated nodes

------------------------------------------------------------

#Ubiquiti UniFi U6+ Access Point
Role: Wireless access for segmented VLANs
Notes:
- Receives all VLANs over tagged trunk
- Broadcasts 5 SSIDs, each mapped to a VLAN
  LAB-WIFI   → VLAN 20
  HOME-WIFI  → VLAN 30
  IOT-WIFI   → VLAN 40
  GUEST-WIFI → VLAN 50
  DMZ-WIFI   → VLAN 60
- LAN VLAN (10) is not available over wireless

------------------------------------------------------------

#Plex Media Server
Role: Media streaming and throughput test
Notes:
- Deployed early for static IP and port forwarding validation
- Moved to isolated VLAN with firewall-restricted access

------------------------------------------------------------

#Lab Workstation
Role: Primary admin and configuration node
Notes:
- Accesses firewall, switch, and AP
- Hosts configuration backups and test scripts
- May run Netdata or monitoring in future phases

------------------------------------------------------------

#Wireless Clients (Laptops, Phones, Tablets)
Role: Endpoint testing devices
Notes:
- Spread across VLANs based on SSID selection
- Used to validate segmentation, wireless isolation, and DNS behavior

------------------------------------------------------------

#Raspberry Pi 4 (Optional Utility Node)
Role: Reserved for future use
    Used for WAP controller via Docker container
Notes:
- May be used for DNS caching, syslog collection, or lightweight observability

------------------------------------------------------------

#Legacy Devices (Phase 1 - Retired)

GL.iNet Flint AX1800 Router
- Served as initial OpenWrt-based router
- Used for early DHCP and firewall learning
- No longer in use

Technicolor CGM4140COM Gateway
- ISP-provided all-in-one box
- Locked firmware, no segmentation or control
- Fully retired from the network

