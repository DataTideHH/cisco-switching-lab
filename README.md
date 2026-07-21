# Cisco Switching Lab

Physical Cisco Catalyst 3560CX lab documenting secure management, IOS maintenance, time synchronization, CCNA-oriented switching practice and the planned network foundation for a future virtualization host.

Project page: https://datatidehh.github.io/cisco-switching-lab/

## Purpose

This repository documents a small physical Cisco lab with an emphasis on reproducible procedures, verification and public-safe technical documentation.

The project supports my Data/BI-oriented portfolio by demonstrating the infrastructure fundamentals behind operational systems and the data they produce. It is not presented as a production network or as a change of specialization into network administration.

A future Proxmox host may later be connected as a lab service platform. That integration is currently a documented roadmap only: no dedicated Proxmox hardware or verified Proxmox deployment is claimed by this repository.

## Current Verified Baseline

The current physical lab uses a Cisco Catalyst `WS-C3560CX-8PC-S`.

Verified as of July 2026:

- console access from macOS through a USB-to-serial adapter
- SSH access for normal administration
- Cisco IOS `15.2(7)E14`
- bootloader `15.2(7r)E`
- primary and fallback IOS images configured
- IOS image integrity checked before activation
- local administrative secrets migrated to Type 9
- NTP synchronization through a local network time source
- CET/CEST timezone configuration
- active Gigabit Ethernet links negotiating at 1 Gbit/s full duplex
- interface error counters checked after the upgrade
- POST, logging and reachability checks completed successfully

Real addresses, hostnames, serial numbers, MAC addresses, credentials and private topology details are intentionally excluded.

## Repository Scope

### Completed foundation

- hardware and software baseline
- console and SSH management
- IOS upgrade and rollback preparation
- basic management hardening
- NTP and timezone configuration
- post-change validation

### Planned CCNA-oriented labs

- VLANs and access ports
- 802.1Q trunks
- Spanning Tree Protocol
- EtherChannel with LACP
- management VLAN design
- inter-VLAN routing
- ACL and troubleshooting exercises
- future expansion with a second switch and a Cisco IOS/IOS XE router
- staged network integration for a future Proxmox virtualization host

The Proxmox-related work remains limited to network design, segmentation and validation. Hypervisor installation, VM and LXC lifecycle, storage, backup and API automation belong in the planned separate [`proxmox-virtualization-lab`](https://github.com/DataTideHH/proxmox-virtualization-lab) repository.

## Documentation

| Document | Purpose |
|---|---|
| [Lab scope](docs/00-lab-scope.md) | Boundaries, learning goals and portfolio role |
| [Hardware inventory](docs/01-hardware-inventory.md) | Current verified device and planned expansion |
| [Topology](docs/02-topology.md) | Public-safe current and future topology |
| [Initial baseline](docs/03-initial-baseline.md) | Baseline and validation commands |
| [VLAN and trunk lab](docs/04-vlan-and-trunk-lab.md) | Planned Layer 2 segmentation lab |
| [Spanning Tree lab](docs/05-spanning-tree-lab.md) | Planned loop-prevention lab |
| [EtherChannel lab](docs/06-etherchannel-lab.md) | Planned link-aggregation lab |
| [Inter-VLAN routing](docs/07-inter-vlan-routing-3560cx.md) | Planned Layer 3 switching lab |
| [Basic switch security](docs/08-basic-switch-security.md) | Management and hardening notes |
| [IOS upgrade workflow](docs/09-ios-upgrade-workflow.md) | Sanitized, verified maintenance workflow |
| [NTP and time synchronization](docs/10-ntp-and-time-synchronization.md) | Local time-source architecture and verification |
| [Proxmox network integration roadmap](docs/11-proxmox-network-integration-roadmap.md) | Planned staged connection of a future virtualization host |
| [Lessons learned](docs/99-lessons-learned.md) | Practical findings from the physical lab |

## Relationship to Connected Labs

This repository focuses on the physical device, Cisco CLI, switching concepts and operational maintenance.

The planned [`proxmox-virtualization-lab`](https://github.com/DataTideHH/proxmox-virtualization-lab) will focus on the future virtualization host, virtual machines, LXC containers, storage, backup, access control and API-based inventory. It does not exist as an implemented hardware lab yet.

The related [network-operations-data-lab](https://github.com/DataTideHH/network-operations-data-lab) focuses on transforming sanitized operational records from network infrastructure and, later, virtualization infrastructure into structured sample data, Python workflows, SQL checks, data-quality reports and BI-oriented outputs.

## Public-Safety Policy

Do not publish:

- credentials or password hashes
- private keys or SSH host keys
- full raw running configurations
- serial numbers or full MAC addresses
- real management IP addresses
- public IP addresses or VPN addresses
- private hostnames and device descriptions
- complete real home-network topology
- real hypervisor API tokens, cluster fingerprints or backup credentials

Use placeholders and sanitized examples throughout the repository.

## Status

Active physical learning lab. The management and maintenance baseline is verified; the multi-switch VLAN, STP and EtherChannel stages are planned as the next expansion. Proxmox integration is a future roadmap item pending suitable dedicated x86 hardware.