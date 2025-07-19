# Homelab-Build

A documentation-first blueprint for building a secure and segmented home lab environment from the ground up. This project tracks the full transformation from an ISP-issued all-in-one gateway into a purpose-built, enterprise-style network designed for learning, working, and experimenting safely at home.

## About This Project

This repository documents the step-by-step build of my personal home lab and segmented network. It began with a basic ISP setup using a Technicolor CGM4140COM gateway, which provided very little transparency, control, or security. I replaced that setup with my own hardware: an ARRIS S34 cable modem and a GL.iNet Flint AX1800 WiFi 6 router. This gives me a clean and fully controlled foundation to build upon.

## Current State (Phase 1)

The Flint router currently manages routing and basic firewall duties. I monitor traffic directly through Flint’s built-in interface. A Plex media server is already up and running on the new LAN, and there is early-stage segmentation between devices.

In parallel, I have been experimenting with a mock-up of the future system using a second mini PC. This device is being used to test OPNsense firewall configurations and layout planning. Although it does not have the performance or I/O needed for the final setup, it has been a helpful tool for learning and preparation.

## Next Steps (Planned Phase 2)

The next major step is to deploy a Protectli mini PC running OPNsense. This will serve as the primary firewall and router. Alongside that, a managed TP-Link switch will allow for VLAN-based segmentation across the network. Once this is in place, the Flint router will be converted into a dedicated wireless access point.

The planned network architecture includes:
- A fully air-gapped lab environment for testing and security research
- Separate VLANs for IoT devices, work-from-home machines, and household devices
- Guest networks with isolated access
- VPN and remote access configurations
- Infrastructure support for penetration testing, monitoring, and training labs


## Documentation Map

Documentation and diagrams are organized in the /docs and /diagrams directories:

    docs/introduction.md – project background and purpose
    docs/hardware/ – bill of materials, device roles
    docs/network/ – subnet planning,


## License

This project is part of my public portfolio and is shared openly for others to learn from or build on. All documentation is versioned in plain text and updated as the lab evolves.

