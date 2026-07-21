# Proxmox Network Integration Roadmap

## Status

This document describes a future lab stage. A dedicated x86 host has not yet been acquired, and no operational Proxmox environment is claimed.

## Purpose

The future Proxmox host should provide a controlled service platform for virtualization, Linux administration, database and API labs. This Cisco repository covers only the physical and logical network connection required for that platform.

The hypervisor itself will be documented separately in `proxmox-virtualization-lab`. Sanitized inventory and monitoring data will later be processed in `network-operations-data-lab`.

## Staged Integration

### Stage 0: design before hardware purchase

- define minimum hardware and network-interface requirements
- reserve a lab-only switch port
- decide whether the first connection uses VLAN 20 or VLAN 30
- document recovery and rollback procedures
- keep the productive home LAN unchanged

### Stage 1: simple access-port baseline

- connect the host through one copper Ethernet interface
- configure one switch port as a normal access port
- validate link speed, duplex, reachability and error counters
- keep hypervisor management and initial guests in one controlled lab VLAN
- verify local console access before testing remote administration

### Stage 2: management separation

- move hypervisor management to a dedicated management VLAN
- test switch SVI, gateway and ACL behavior where applicable
- document which devices are allowed to reach the management interface
- confirm that guest networks cannot reach management services unless explicitly allowed

### Stage 3: optional 802.1Q trunk

- configure a dedicated switch port as a trunk
- allow only explicitly required VLANs
- map VLANs to Proxmox Linux bridges or VLAN-aware bridges
- validate native VLAN assumptions and tagging end to end
- keep an independent console recovery path available

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
- STP state is understood and documented

### Layer 3 and management

- management reachability works only from intended sources
- default gateway and DNS behavior are validated
- NTP provides consistent timestamps across switch and hypervisor
- SSH and web management do not require public port forwarding

### Recovery

- local console access is available
- previous switch configuration can be restored
- an access-port fallback is documented before trunk experiments
- real credentials, addresses, fingerprints and tokens are excluded from GitHub

## Repository Boundaries

| Concern | Repository |
|---|---|
| Cisco switch ports, VLANs, trunks and reachability | `cisco-switching-lab` |
| Proxmox installation, bridges, guests, storage and backups | `proxmox-virtualization-lab` |
| API exports, data modelling, checks and BI reporting | `network-operations-data-lab` |

## Portfolio Principle

The goal is not to imitate an enterprise data center. The goal is to demonstrate a small, verified and well-documented chain from physical networking through virtualization to operational data analysis.