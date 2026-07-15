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

## Documentation

### Verified foundation

- [Lab scope](00-lab-scope.md)
- [Hardware inventory](01-hardware-inventory.md)
- [Current and planned topology](02-topology.md)
- [Baseline and validation commands](03-initial-baseline.md)
- [Basic switch security](08-basic-switch-security.md)
- [IOS upgrade workflow](09-ios-upgrade-workflow.md)
- [NTP and time synchronization](10-ntp-and-time-synchronization.md)
- [Lessons learned](99-lessons-learned.md)

### Planned CCNA-oriented labs

- [VLAN and trunk lab](04-vlan-and-trunk-lab.md)
- [Spanning Tree lab](05-spanning-tree-lab.md)
- [EtherChannel lab](06-etherchannel-lab.md)
- [Inter-VLAN routing](07-inter-vlan-routing-3560cx.md)

## Next steps

- add a second Cisco switch for physical trunk, STP and EtherChannel exercises
- introduce dedicated lab VLANs without affecting the normal home network
- add a Cisco IOS or IOS XE router for routing, NAT, DHCP and ACL practice
- continue documenting only verified results and public-safe examples

## Relationship to the data project

This repository focuses on Cisco CLI work, device operation, maintenance and switching concepts.

The related [Network Operations Data Lab](https://datatidehh.github.io/network-operations-data-lab/) focuses on turning sanitized operational records into structured sample data, Python workflows, SQL checks, data-quality reports and BI-oriented outputs.

## Repository

Source code and documentation: [github.com/DataTideHH/cisco-switching-lab](https://github.com/DataTideHH/cisco-switching-lab)
