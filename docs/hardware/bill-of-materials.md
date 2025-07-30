# bill_of_materials.md

Final Hardware Inventory (Phase 2)

This document lists the hardware deployed in the live segmented homelab network. Devices were selected based on reliability, administrative control, firmware transparency, and compatibility with VLANs and firewall isolation.

---

Core Networking Infrastructure

Device: ARRIS S34 DOCSIS 3.1 Cable Modem
Role: Internet bridge
Notes: No routing or WiFi. Runs in pure bridge mode.

Device: Protectli Vault FW6E (4-core, 6-port)
Role: Core firewall and router
Notes: Runs OPNsense with full VLAN support, DNS, DHCP, and interface-specific firewall rules.

Device: TP-Link TL-SG2210MP (Managed Switch)
Role: VLAN trunking and access port isolation
Notes: GUI management, per-port VLAN control, PoE+ support, and link monitoring.

Device: TP-Link TL-SG1210MP (Unmanaged Switch)
Role: Downstream breakout for LAB VLAN devices
Notes: No VLAN control. Used on tagged port with untagged VLAN for static segment.

Device: Ubiquiti UniFi U6+ Access Point
Role: Wireless access with VLAN-bound SSIDs
Notes: Dual-band, ceiling-mounted, supports multiple isolated wireless zones.

---

Internal Service and Test Devices

Device: Plex Media Server (self-built)
Role: Streaming and network testing
Notes: Used to validate port forwarding, static IPs, DNS stability, and throughput under load.

Device: Lab Workstation
Role: Main admin node
Notes: Used for switch/firewall config, remote access, scripting, and log review.

Device: Wireless Client Devices (laptops, phones)
Role: Endpoint testing
Notes: Spread across GUEST, HOME, and LAB SSIDs for segment testing.

Device: Raspberry Pi 4 (Optional Utility Node)
Role: Potential use as syslog, Pi-hole, or monitor
Notes: Reserved for future integration.

---

Legacy (Phase 1) Equipment

Device: GL.iNet Flint AX1800 Router
Role: Former primary router
Notes: Used for early experimentation with OpenWrt, static DHCP, and admin interface control.

Device: Technicolor CGM4140COM
Role: Original ISP gateway
Notes: ISP-provided device with locked-down firmware and minimal visibility. No longer in use.

---

Notes

All key infrastructure operates without cloud control or vendor lock-in. Devices were selected for easy, manual setup using the web GUI or CLI. The Protectli firewall and TP-Link managed switch create the backbone for VLAN segmentation. The access point supports multiple SSIDs linked to specific VLANs and is mounted on the ceiling for the best coverage.
