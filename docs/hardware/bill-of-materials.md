# Bill of Materials (Phase 1)

This document lists the hardware currently deployed in the home network rebuild, along with rationale for each selection. Prices are approximate at the time of purchase and may vary.

---

## Core Networking Hardware

| Device | Model | Role | Notes | Price |
|--------|-------|------|-------|-------|
| Cable Modem | ARRIS S34 DOCSIS 3.1 | Internet bridge | No routing or WiFi — pure bridge mode | ~$185 |
| Router | GL.iNet Flint AX1800 | Primary router and WiFi AP | Full admin access, WiFi 6, OpenWrt-based UI | ~$110 |
| ISP Gateway (Old) | Technicolor CGM4140COM | Replaced | Locked-down ISP combo device | Provided by ISP |

---

## Internal Service Devices

| Device | Role | Notes |
|--------|------|-------|
| Plex Media Server | Self-hosted media | Initial test case for static IPs, port forwarding, and streaming reliability |
| Workstation | Main control node | Used for configuration, remote access, and service management |
| Mobile Devices | Client endpoints | Connect via WiFi, used for everyday traffic testing |

---

## Planned (Phase 2)

| Device | Model | Role | Notes | Price (Est.) |
|--------|-------|------|-------|--------------|
| Firewall Appliance | Protectli FW4B or FW6B | Core router/firewall | To run OPNsense with VLANs, IDS, and VPN support | ~$300–$500 |
| Managed Switch | TP-Link TL-SG2008 or similar | VLAN trunking + port isolation | Layer 2 segmentation with GUI control | ~$70 |
| Access Point | Ubiquiti U6+ or similar | Isolated WiFi zones | VLAN-capable, enterprise-grade wireless | ~$120 |

---

## Notes

- Devices were selected for long-term use, open firmware support, and vendor-neutral architecture
- The entire Phase 1 stack runs without cloud-based configuration or vendor lock-in
- Plex server is wired when possible to test consistent throughput under load

