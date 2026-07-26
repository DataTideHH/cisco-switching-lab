---
layout: default
title: Cisco Switching Lab
description: Physical Cisco Catalyst 3560CX lab for secure management, IOS maintenance and CCNA-oriented switching practice.
---

# Cisco Switching Lab

A documented physical Cisco Catalyst 3560CX learning lab focused on secure management, controlled IOS maintenance, verification and CCNA-oriented switching fundamentals.

This is a supporting infrastructure project for my Data/BI-oriented portfolio. It demonstrates careful technical work, reproducible procedures and troubleshooting without presenting the lab as a production network or network-consulting service.

## Current verified baseline

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
- active Gigabit Ethernet links verified at 1 Gbit/s full duplex
- interface error counters, POST results, logging and reachability checked after the upgrade

Real addresses, hostnames, serial numbers, MAC addresses, credentials and private topology details are intentionally excluded.

## Platform lifecycle

Cisco has announced end of sale and end of life for the `WS-C3560CX-8PC-S`. The published last date of support is **30 April 2029**.

The switch remains useful as a controlled physical IOS and CCNA-oriented learning platform. It is not presented as a recommendation for a new production deployment.

## Planned VLAN roles

| VLAN | Purpose |
|---:|---|
| 10 | test clients |
| 20 | lab systems |
| 30 | test services and servers |
| 99 | management |
| 998 | unused native VLAN for lab trunks |
| 999 | parking VLAN for unused access ports |

VLAN 998 is planned only as the matching native VLAN on both ends of isolated lab trunks. It should have no SVI and no connected end devices. VLAN 99 remains the management VLAN.

## Documentation

### Verified foundation

- [Lab scope](00-lab-scope.md)
- [Hardware inventory and lifecycle](01-hardware-inventory.md)
- [Current and planned topology](02-topology.md)
- [Baseline and validation commands](03-initial-baseline.md)
- [Basic switch security](08-basic-switch-security.md)
- [IOS upgrade workflow](09-ios-upgrade-workflow.md)
- [NTP and time synchronization](10-ntp-and-time-synchronization.md)
- [Official references and learning resources](12-official-references.md)
- [Lessons learned](99-lessons-learned.md)

### Planned CCNA-oriented labs

- [VLAN and trunk lab](04-vlan-and-trunk-lab.md)
- [Spanning Tree lab](05-spanning-tree-lab.md)
- [EtherChannel lab](06-etherchannel-lab.md)
- [Inter-VLAN routing](07-inter-vlan-routing-3560cx.md)
- [Proxmox network integration roadmap](11-proxmox-network-integration-roadmap.md)

The planned lab documents now use a consistent method: prerequisites, initial baseline, change plan, verification, success criteria, rollback, evidence and safety boundaries.

## Next steps

- add a second compatible Cisco switch for physical trunk, STP and EtherChannel exercises
- introduce dedicated lab VLANs without affecting the normal home network
- use a separate unused native VLAN rather than the management VLAN on lab trunks
- add a Cisco IOS or IOS XE router for routing, NAT, DHCP and ACL practice
- continue documenting only verified results and public-safe examples

## Connected portfolio projects

- [IPv4 Subnet Calculator Multilang](https://datatidehh.github.io/ipv4-subnet-calculator-multilang/) — tested IPv4/CIDR logic in Java, C++ and Python
- [Spring Boot Process API Basics](https://datatidehh.github.io/spring-boot-process-api-basics/) — small layered Java REST API for structured operational records
- [Network Operations Data Lab](https://datatidehh.github.io/network-operations-data-lab/) — sanitized operational records, Python, SQL, data quality and BI-oriented outputs
- [`proxmox-virtualization-lab`](https://github.com/DataTideHH/proxmox-virtualization-lab) — future dedicated virtualization project; no implemented hardware lab is claimed yet
- [`open-learning-resources`](https://github.com/DataTideHH/open-learning-resources) — curated Cisco, Networking Academy and RFC references used alongside this lab

## Repository

Source code and documentation: [github.com/DataTideHH/cisco-switching-lab](https://github.com/DataTideHH/cisco-switching-lab)