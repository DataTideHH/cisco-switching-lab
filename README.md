# Cisco Switching Lab

Documented Cisco switching lab using a Cisco Catalyst 3560CX and a Cisco Catalyst 2950SX for practicing CCNA-level switching concepts.

## Purpose

This repository documents a small physical switching lab focused on VLANs, trunking, Spanning Tree Protocol, EtherChannel, switch management, basic Layer 3 switching and troubleshooting.

The goal is not to present a production network, but to document practical learning steps in a clear and reproducible way.

## Lab Scope

This project is part of my DataTideHH learning and portfolio setup. It complements my data, SQL, Python and BI projects by documenting practical network infrastructure fundamentals.

The lab focuses on:

- VLANs
- 802.1Q trunking
- Spanning Tree Protocol
- EtherChannel / LACP
- switch management
- basic switch hardening
- basic Layer 3 switching on the Catalyst 3560CX
- troubleshooting and documentation

## Hardware

Planned lab hardware:

- Cisco Catalyst 3560CX-8PC-S
- Cisco Catalyst WS-C2950SX-24
- Cisco-compatible 1000BASE-SX SFP module
- MT-RJ to LC multimode fiber patch cable
- Ethernet patch cables
- macOS / Windows / Linux clients for testing

## Planned Topology

    Client / Test Device
            |
            | access port
            |
    Cisco Catalyst 2950SX-24
            |
            | 1000BASE-SX fiber trunk
            |
    Cisco Catalyst 3560CX-8PC-S
            |
            | uplink / management / lab network
            |
    Existing home or lab network

## Planned Labs

1. Hardware inventory and baseline checks
2. Initial switch access and management
3. VLAN basics
4. 802.1Q trunk between both switches
5. STP behavior
6. EtherChannel / LACP
7. Basic switch security
8. Inter-VLAN routing on the Catalyst 3560CX
9. Troubleshooting notes and lessons learned

## Documentation Policy

Sensitive values are redacted before publication.

Do not publish:

- serial numbers
- full MAC addresses unless needed and anonymized
- credentials
- private keys
- public IP addresses
- real VPN or Tailscale addresses
- full raw running configurations containing private information

Use placeholders such as:

- SERIAL_REDACTED
- MAC_REDACTED
- 192.168.99.x
- 100.x.y.z
- PASSWORD_REDACTED

## Status

Initial scaffold created. Hardware baseline and configuration documentation will be added after the switches are connected and verified.
