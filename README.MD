[[/CharlesX0101]](https://charlesx0101.com/) [[/About]](http://charlesx0101.com/about) [[/Labs]](https://charlesx0101.com/labs) [[/Projects]](https://charlesx0101.com/projects) [[/Contact]](https://charlesx0101.com/contact) 
# Homelab Build

A documentation-first plan for creating a secure and separate home lab environment from scratch. This project follows the complete change from an ISP-issued all-in-one gateway to a custom, enterprise-level network made for learning, working, and experimenting safely at home.

## About This Project

This repository documents the complete design, build, and deployment of my personal home lab and segmented network. The original setup began with a Technicolor CGM4140COM gateway provided by the ISP, which offered limited control and transparency. It was then replaced with an ARRIS S34 cable modem and a GL.iNet Flint AX1800 WiFi 6 router. This new setup provided a cleaner and more flexible platform for experimentation.

What started as a flat network evolved into a fully segmented infrastructure that features VLAN isolation, firewall enforcement, and organized wireless zones. This project shows the completion of that transition. The network is now live and in use. It is designed to match enterprise standards while still being manageable at home.

## Current State (Phase 2 - Complete)

The lab now operates on a secure and well-organized infrastructure with these components::

- Protectli Vault FW6E mini PC running OPNsense as the core firewall and router
- TP-Link TL-SG2210MP managed switch configured with VLAN trunking and tagged access ports
- VLAN design includes isolated zones for LAN, LAB, HOME, IOT, GUEST, and DMZ environments
- Ubiquiti U6+ wireless access point configured with multiple SSIDs mapped to VLANs
- Static IP reservations and segmented DHCP scopes per VLAN
- Firewall rules tailored for strict access control and inter-VLAN traffic enforcement
- Full wired and wireless coverage with infrastructure for testing, monitoring, media, and experimentation

This environment supports several simultaneous use cases. These include isolated security labs, smart home containment, guest access, and regular production workstations. All traffic paths have been tested and confirmed.

## Final Network Architecture

The current production setup includes:

- VLAN 10: LAN – Admin and core systems
- VLAN 20: LAB – Test VMs and isolated tooling
- VLAN 30: HOME – Daily-use personal devices
- VLAN 40: IOT – Smart devices, speakers, displays
- VLAN 50: GUEST – Guest WiFi network
- VLAN 60: DMZ – Exposed services and honeypots

All VLANs connect from the OPNsense firewall to the managed switch. Wireless SSIDs link directly to VLANs at the access point. Firewall rules separate traffic by default, with clear exceptions when necessary.

## Documentation Map

Documentation and diagrams are organized in the /docs and /diagrams directories:

    docs/introduction.md         – project background and purpose
    docs/hardware/               – bill of materials, device roles
    docs/network/                – VLAN and subnet design, IP schema
    docs/firewall_setup.md       – interface assignments, rulesets
    docs/switch_config.md        – port tagging and trunking layout
    docs/wireless_layout.md      – UniFi setup and VLAN SSID mapping
    docs/testing_procedure.md    – validation steps and ping results
    docs/lessons_learned.md      – configuration notes and caveats

## License

This project is part of my public portfolio and is shared openly for others to learn from or build on. All documentation is versioned in plain text and reflects the final production state of the live environment.

