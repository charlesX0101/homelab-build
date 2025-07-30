# core-services.md

Core Services

This document outlines all internal services currently deployed or planned in the
segmented homelab network. Each service is defined by its function, location,
access policy, and VLAN assignment. Services are tightly segmented and access is
granted only through explicit firewall rules.

------------------------------------------------------------

Currently Running

Service: Plex Media Server
Purpose: Stream local media to clients on the HOME and LAB VLANs
Location: Static IP in VLAN 20 (LAB)
Access:
  - Accessible from VLAN 10 (Admin) and VLAN 30 (HOME)
  - Blocked from IOT, GUEST, and DMZ VLANs
  - External access via TCP 32400 (optional port forwarding)
Notes:
  - Validated during initial testing
  - Serves as real-world test for DNS, static IPs, and throughput

Service: DNS Resolver (Unbound via OPNsense)
Purpose: Local DNS for hostname overrides and internal resolution
Location: OPNsense, VLAN 10 interface
Access:
  - All VLANs may query DNS resolver
  - Cross-VLAN DNS queries are blocked
Notes:
  - DNS entries defined via OPNsense overrides
  - May eventually move to Pi-hole or separate resolver

Service: DHCP (Per VLAN via OPNsense)
Purpose: Issue IPs and define default gateway per interface
Location: OPNsense interface-based scopes
Access:
  - Each VLAN receives DHCP only from its assigned interface
Notes:
  - Static leases defined for Plex, firewall, AP, and switch

------------------------------------------------------------

Planned Services

Service: WireGuard VPN (Remote Access)
Purpose: Secure remote entry into Admin VLAN or lab infrastructure
Location: OPNsense, VLAN 10
Access:
  - Restricted to authenticated clients only
  - UDP port exposed via WAN ruleset
Notes:
  - VPN clients may be assigned a virtual IP scope
  - Access limited by interface group and firewall rules

Service: IDS/IPS (Suricata or Zenarmor)
Purpose: Traffic inspection and behavioral alerting
Location: OPNsense (hosted directly)
Scope:
  - All VLANs monitored
  - Priority on GUEST, IOT, and DMZ zones
Notes:
  - Logging retained for abnormal flows and scans

Service: Monitoring Dashboard
Purpose: Track uptime, bandwidth, and system health
Candidates: Netdata, Uptime Kuma, LibreNMS
Location: VLAN 10 (Admin) or VLAN 60 (DMZ utility node)
Access:
  - Access restricted to VLAN 10 only
  - Web access over HTTP/HTTPS, SSH optional
Notes:
  - Used to monitor Plex, firewall, WAP, and LAN services

Service: Reverse Proxy (Optional)
Purpose: Internal routing via clean subdomains (e.g. plex.local)
Candidates: Caddy, Nginx Proxy Manager
Location: Trusted host in VLAN 10
Access:
  - Not yet deployed
  - Internal use only
Notes:
  - May terminate TLS locally
  - Useful for simplifying port and IP routing

------------------------------------------------------------

Notes

- All service hosts are or will be assigned static IPs
- Firewall rules explicitly control which VLANs may reach each service
- Services are not accessible from GUEST, IOT, or DMZ unless required
- No service runs with WAN exposure by default
- Backup and recovery information is stored separately in secure storage

