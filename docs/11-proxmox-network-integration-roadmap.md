# Proxmox Network Integration Roadmap

## Status

This document describes a future lab stage. A dedicated x86 host has not yet been acquired, and no operational Proxmox environment is claimed.

## Purpose

The future Proxmox host should provide a controlled service platform for virtualization, Linux administration, database and API labs. This Cisco repository covers only the physical and logical network connection required for that platform.

The hypervisor itself will be documented separately in [`proxmox-virtualization-lab`](https://github.com/DataTideHH/proxmox-virtualization-lab). Sanitized inventory and monitoring data will later be processed in `network-operations-data-lab`.

## Planned VLAN Roles

| VLAN | Role |
|---:|---|
| 20 | initial lab access network |
| 30 | later service and server network |
| 99 | later dedicated management network |
| 998 | unused native VLAN for an optional trunk |
| 999 | parking VLAN for unused switch access ports |

VLAN 998 should not have an SVI or connected end devices. VLAN 99 remains a tagged management VLAN when a trunk is introduced; it is not reused as the native VLAN.

## Staged Integration

### Stage 0: design before hardware purchase

- define minimum hardware and network-interface requirements
- reserve a lab-only switch port
- decide whether the first connection uses VLAN 20 or VLAN 30
- verify that planned subnets do not overlap with the home LAN, VPNs or other labs
- document recovery and rollback procedures
- keep the productive home LAN unchanged

### Stage 1: simple access-port baseline

- connect the host through one copper Ethernet interface
- configure one switch port as a normal access port
- validate link speed, duplex, reachability and error counters
- keep hypervisor management and initial guests in one controlled lab VLAN
- verify local console access before testing remote administration
- record the switch port, host interface and bridge relationship using sanitized identifiers

### Stage 2: management separation

- move hypervisor management to dedicated VLAN 99
- test switch SVI, gateway and ACL behavior where applicable
- document which devices are allowed to reach the management interface
- confirm that guest networks cannot reach management services unless explicitly allowed
- retain a local host console or access-port recovery path

### Stage 3: optional 802.1Q trunk

- configure a dedicated switch port as a static trunk
- use VLAN 998 as the matching unused native VLAN on both ends
- carry management VLAN 99 and required service VLANs as tagged VLANs
- allow only explicitly required VLANs, including VLAN 998 for the native role
- map tagged VLANs to Proxmox Linux bridges or VLAN-aware bridges
- validate native VLAN assumptions and tagging end to end
- confirm that VLAN 998 has no SVI and no endpoint traffic
- keep an independent console and access-port recovery path available

Conceptual switch-side pattern:

```text
interface GigabitEthernet0/X
 description FUTURE_PROXMOX_TRUNK
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 20,30,99,998
 no shutdown
```

The exact interface and allowed VLAN list must match the final host design and must be verified before use.

### Stage 4: operational data export

- collect sanitized node, interface and guest inventory through the Proxmox API
- store synthetic or anonymized examples only
- correlate physical switch ports with virtual infrastructure records
- pass the exported data to `network-operations-data-lab`

## Planned Validation Checklist

### Physical and Layer 2

- link is up at the expected speed and duplex
- no unexpected CRC, input or output errors appear
- access VLAN or trunk configuration matches the documented design
- only intended VLANs are allowed on a trunk
- native VLAN 998 matches on both ends and has no endpoint use
- management VLAN 99 remains tagged on the trunk
- STP state is understood and documented

### Layer 3 and management

- management reachability works only from intended sources
- default gateway and DNS behavior are validated
- NTP provides consistent timestamps across switch and hypervisor
- SSH and web management do not require public port forwarding
- guest and service networks cannot reach management unless explicitly permitted

### Recovery

- local console access is available
- previous switch configuration can be restored
- an access-port fallback is documented before trunk experiments
- the host can be returned to the known single-VLAN baseline
- real credentials, addresses, fingerprints and tokens are excluded from GitHub

## Repository Boundaries

| Concern | Repository |
|---|---|
| Cisco switch ports, VLANs, trunks and reachability | `cisco-switching-lab` |
| Proxmox installation, bridges, guests, storage and backups | [`proxmox-virtualization-lab`](https://github.com/DataTideHH/proxmox-virtualization-lab) |
| API exports, data modelling, checks and BI reporting | `network-operations-data-lab` |

## Portfolio Principle

The goal is not to imitate an enterprise data center. The goal is to demonstrate a small, verified and well-documented chain from physical networking through virtualization to operational data analysis.