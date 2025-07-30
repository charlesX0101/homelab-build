# firewall-rules.md

##Firewall Rules

This document outlines the firewall policy and enforcement strategy for the
segmented homelab network. Rules are implemented through OPNsense and applied to
VLAN-tagged interfaces using a deny-by-default, allow-by-exception model.

------------------------------------------------------------

#Global Policy

- All inter-VLAN traffic is blocked by default.
- Outbound internet access is allowed for all VLANs unless otherwise noted.
- Inbound internet traffic is blocked entirely unless explicitly port-forwarded.
- The OPNsense Web UI is accessible only from VLAN 10 (LAN - Admin).

------------------------------------------------------------

#VLAN-to-VLAN Access Rules

From VLAN 10 (LAN - Admin):
  - Full access to all VLANs for diagnostics, GUI access, SSH, and backups.

From VLAN 20 (LAB):
  - Access to VLAN 10 is restricted. Only allowed to reach the network monitor
    located on switch port 5 (specific IP and VLANID).
  - No access to other VLAN 10 systems or the firewall interface.
  - Outbound internet allowed for updates, repositories, and downloads.
  - Access to DNS and NTP is permitted.

From VLAN 30 (HOME):
  - No access to VLAN 10 (Admin) or VLAN 20 (LAB).
  - Allowed access to the Plex server on VLAN 20.
  - Full outbound internet access.

From VLAN 40 (IOT):
  - Denied access to all internal VLANs.
  - Outbound internet allowed for updates, cloud sync, and telemetry.
  - NTP and DNS requests allowed outbound.

From VLAN 50 (GUEST):
  - Fully isolated. No access to any internal resources.
  - Outbound internet only. No access to local DNS or internal gateways.

From VLAN 60 (DMZ):
  - No access to VLAN 10 or any private VLANs.
  - Outbound internet access allowed.
  - Access allowed to honeypot or monitoring tools if defined by rule.

------------------------------------------------------------

#Service Port Access

Plex Media Server (VLAN 20 - LAB):
  - Local access from VLAN 10 (LAN) and VLAN 30 (HOME)
  - Internet access via TCP 32400 (if port-forwarded through OPNsense)

OPNsense Web UI:
  - TCP 443
  - Accessible only from VLAN 10
  - Blocked explicitly on all other interfaces

DNS:
  - Centralized through OPNsense (unbound resolver or forwarding)
  - DNS requests allowed outbound from all VLANs
  - No cross-VLAN DNS allowed unless explicitly required

NTP:
  - Outbound NTP allowed from all VLANs

Syslog / Monitoring:
  - Reserved for future use on VLAN 60 (DMZ) or a utility node
  - To be explicitly whitelisted when implemented

------------------------------------------------------------

#Logging and Alerting

- All blocked inter-VLAN access attempts are logged.
- High-frequency or lateral movement attempts from VLANs 40 or 50 trigger alerts.
- Any access attempt toward VLAN 10 (Admin) from unauthorized VLANs is logged.
- Firewall ruleset is backed up and versioned offline for recovery.

------------------------------------------------------------

#Management Notes

- Rules are managed per VLAN interface inside OPNsense.
- LAN (VLAN 10) is treated as the trusted management zone.
- No pass rules are defined in floating rules unless explicitly necessary.
- Internal DNS mappings are resolved locally where possible to avoid external
  resolution leaks.

