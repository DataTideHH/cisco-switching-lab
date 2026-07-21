# Lab Scope

## Goal

This lab is a small physical Cisco environment for CCNA-oriented switching, management and troubleshooting practice.

The purpose is to connect networking theory with verified command-line work on real hardware while keeping experiments separated from the normal home network.

## Why This Lab Exists

As part of my retraining as a Fachinformatiker für Daten- und Prozessanalyse, networking fundamentals matter because data platforms, BI systems, virtualization hosts and applications depend on reliable infrastructure.

The lab provides the physical network context for two connected portfolio layers:

- the related `network-operations-data-lab`, where sanitized operational records are transformed into structured data, SQL checks and BI-oriented outputs
- the planned `proxmox-virtualization-lab`, which will document a future dedicated virtualization host after suitable x86 hardware is available

The Proxmox connection is currently an architecture roadmap only. This repository does not claim that a Proxmox host has already been installed or validated.

## In Scope

- Cisco IOS fundamentals
- device inventory and baseline checks
- console and SSH management
- IOS maintenance and rollback preparation
- NTP and log-time consistency
- VLAN creation and verification
- access ports and 802.1Q trunks
- STP and Layer 2 loop prevention
- EtherChannel and LACP
- basic switch hardening
- inter-VLAN routing on the Catalyst 3560CX
- future router labs with routing, NAT, DHCP and ACLs
- planned network segmentation for a future virtualization host
- access-port-first and optional later trunk-based Proxmox connectivity
- troubleshooting and reproducible documentation

## Out of Scope

- presenting the lab as a production network
- exposing private network details or credentials
- uncontrolled experiments on the productive home LAN
- simulating enterprise scale without a concrete learning purpose
- presenting DataTideHH as a network consultancy
- documenting unverified Proxmox installation results
- hypervisor, VM, LXC, storage or backup administration, which belongs in the future `proxmox-virtualization-lab`

## Intended Portfolio Role

This is a supporting infrastructure project for a Data/BI-oriented profile. It demonstrates technical care, controlled changes, validation, troubleshooting and documentation rather than a change of specialization into network administration.

The future Proxmox integration should strengthen this role by showing how a physical network layer can support virtualized services and generate operational data for a separate Data/BI workflow.