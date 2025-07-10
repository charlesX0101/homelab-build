# Introduction

This document provides the context, reasoning, and architectural thinking behind the `homelab-build` project. It serves as both a design narrative and a reference for others planning a similar network transition.

---

## From Consumer Hardware to Controlled Infrastructure

This project began out of necessity — the default home network was built around a Technicolor CGM4140COM “Panoramic WiFi Gateway” provided by my ISP. While this device worked for basic connectivity, it was a black box:

- No access to routing tables or meaningful firewall controls
- No VLAN support or traffic segmentation
- ISP-locked firmware with minimal customization
- No realistic way to grow into a secure lab or internal service host

That system was acceptable for casual browsing and streaming. But for self-hosting, security training, and long-term network management, it was a dead end.

---

## Starting Over — The First Real Build

The first step was full separation of modem and routing layers:

- **ARRIS S34 DOCSIS 3.1 Cable Modem:** A stripped-down, bridge-only modem — no built-in NAT, no WiFi, no distractions.
- **GL.iNet Flint AX1800 Router:** A WiFi 6 router running a modern OpenWrt-based firmware with full admin access, DNS control, DHCP configuration, and firewall rule customization.

This gave me clean control over the LAN and opened up possibilities for service hosting.

---

## Initial Services: Plex Media Server

Rather than just plan for an abstract network, I put it to real use immediately by setting up a Plex Media Server on the new LAN.

This was important because it helped validate:
- Port-forwarding configuration
- LAN-wide DNS reliability
- Static addressing
- Latency and throughput under real media loads

The media server acts as both a utility and a live test environment for future segmentation efforts.

---

## Design Thinking: Preparing for Phase 2

This project isn’t just about replacing hardware — it's about building a proper internal network architecture. That means:

- **Control and Visibility** — DNS, DHCP, firewall logs, routing tables
- **Segmentation** — separating IoT, media, workstations, and guest traffic
- **Scalability** — adding services without collapsing into flat chaos
- **Security** — reducing lateral movement, isolating high-value targets

The current Phase 1 network is still flat — but controlled. That’s the critical difference from the original setup: it’s mine, and I can shape it.

---

## Where This Is Going

The next major step is transitioning to a segmented environment using OPNsense running on a Protectli mini PC. That will allow:

- VLAN-based segmentation across switches and APs
- Inter-VLAN firewall rules
- Dedicated VPN tunnels
- Intrusion detection and monitoring
- Uptime-aware service zones (media, work, etc.)

Rather than rushing this transition, I’m treating it like a full infrastructure project — including diagrams, configuration templates, and documentation at every stage.

---

## Notes on Methodology

This repository reflects a real build process — not a tutorial, not a product, and not a "lab in a box." It’s intentionally documented with:

- Real hardware
- Actual services running
- Evolving configurations
- Thought-out templates and diagrams

It’s designed to be forked, studied, and reinterpreted — but not blindly copied.


