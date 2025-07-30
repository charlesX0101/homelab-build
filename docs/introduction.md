# introduction.md

## Project Introduction

This project describes the complete change of my home network from a simple, consumer-grade setup to a secure, fully segmented, enterprise-level system. It is a real, working environment, designed, built, documented, and deployed in stages, with the final result now fully operational.

This is not a prepackaged lab or a simulation. The configurations, services, and diagrams show real hardware and active infrastructure.

## From Consumer Hardware to Controlled Infrastructure

The original network relied on a Technicolor CGM4140COM "Panoramic WiFi Gateway" from the ISP. It worked for casual browsing, but it quickly became a bottleneck for more serious tasks. It was a locked-down device that provided little visibility or control:

- No access to routing tables or meaningful firewall rule creation
- No VLAN support or traffic segmentation
- ISP firmware with no ability to monitor logs or enable service growth
- No pathway to build out internal tools or isolated labs

That system worked fine for streaming and basic access. However, it was not suitable for training, self-hosting, and long-term infrastructure planning.

## The First Real Build

The first milestone was separating the routing and modem layers:

- ARRIS S34 DOCSIS 3.1 Modem – no NAT, no wireless, fully bridge-only
- GL.iNet Flint AX1800 Router – a WiFi 6 router with OpenWrt-based firmware, admin access, DNS control, DHCP customization, and basic firewall tuning

This allowed me to have clear control over the LAN. It set the stage for deploying services and keeping internal elements separate.

## Early Testing with Plex Media Server

Before completely changing the network, I set up a Plex Media Server on the new LAN. This gave me real-world feedback on:

- Port forwarding logic
- DNS resolution across static and dynamic devices
- Address reservations
- Network performance under sustained media traffic

This approach showed that the new routing layer could support internal services. It also provided me with a functional testbed as I planned the segmented rebuild.

## Planning the Transition to Phase 2

The project was never only about better hardware. It was about creating a genuine internal network, with professional design goals:

- DNS, DHCP, and firewall visibility
- Logical traffic segmentation across zones
- Support for internal services, VPN access, and experimentation
- Reduction of lateral movement between device types and VLANs
- Administrative control and isolation across all layers

Phase 1 gave me complete control. Phase 2 built on that foundation and turned it into a strong, production-ready platform.

## Final Infrastructure Overview (Phase 2 Complete)

The network is now built around the following core elements:

- OPNsense firewall running on a Protectli FW6E mini PC
- TP-Link TL-SG2210MP managed switch configured with VLAN trunk and tagged access ports
- VLANs for LAN, LAB, HOME, IOT, GUEST, and DMZ
- UniFi U6+ access point with SSID-to-VLAN mapping
- Isolated DHCP pools, DNS resolution per segment, and strict firewall rules
- All GUI management interfaces accessible from designated admin VLANs only

This infrastructure supports remote access, honeypots, media streaming, segmented wireless, and safe experimentation. They all run in parallel without compromising integrity.

## Documentation Philosophy

This repository is a real design record, not a tutorial. It contains:

- Actual configs from deployed devices
- Infrastructure diagrams created for real planning
- Tools, tests, and results from real deployments
- Notes and mistakes from each step of the process

It is meant to be forked, adapted, or studied, but not copied without thought. It shows the mindset and methods used to build secure, modular infrastructure from the ground up.
