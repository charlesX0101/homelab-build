# Core Services

This document details the self-hosted and internal services that run within the homelab environment. Each service is mapped to its function, host location, network policy, and VLAN assignment.

---

## Currently Running

### Plex Media Server

- **Purpose:** Stream local media to devices across the network and optionally external clients.
- **Location:** Static IP in VLAN 20 (Media)
- **Access Control:**
  - Accessible from Admin VLAN and Media VLAN only
  - External access via port forwarding on TCP 32400 (optional)
- **Notes:** Validates port forwarding, DNS, and LAN throughput

---

## Planned Services

### Internal DNS Resolver

- **Purpose:** Provide authoritative DNS for internal hostnames and override upstream resolution.
- **Host:** OPNsense DNS Resolver or Pi-hole on VLAN 10
- **Access:** All VLANs use this resolver; inter-VLAN DNS traffic is restricted by rule

---

### WireGuard VPN Gateway

- **Purpose:** Secure remote access to the entire homelab from outside the network
- **Location:** OPNsense in VLAN 10
- **Access:** Requires key-based authentication and firewall pinhole (UDP port)

---

### IDS/IPS (Suricata or Zenarmor)

- **Purpose:** Monitor and inspect traffic for signs of intrusion or abuse
- **Location:** OPNsense
- **Monitoring Scope:** All VLANs, with special attention on IoT and Guest traffic

---

### Reverse Proxy (Optional)

- **Purpose:** Host internal web services under domain-based routing (e.g. `plex.local`, `admin.local`)
- **Candidates:** Caddy, Nginx Proxy Manager
- **Location:** Trusted device in VLAN 10
- **Use Case:** Clean internal service access, optional TLS termination

---

### Monitoring & Status Dashboard

- **Purpose:** Track uptime, resource usage, and connectivity
- **Candidates:** Uptime Kuma, Netdata, LibreNMS
- **Access:** Admin VLAN only
- **Use Case:** Long-term observability and performance tracking

---

## Notes

- Services will be assigned static IPs and DNS records via central resolver
- VLAN segmentation ensures that services are only reachable where explicitly allowed
- All service hosts will be backed up and mapped in the network inventory


