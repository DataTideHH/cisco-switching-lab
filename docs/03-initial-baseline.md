# Initial Baseline

## Purpose

Before changing any configuration, the initial state of both switches should be documented.

This helps with:

- understanding the previous configuration
- checking hardware and software versions
- identifying interface names
- identifying licensing and image details
- safely resetting or reconfiguring the devices later

## Catalyst 3560CX Baseline Commands

    enable
    terminal length 0
    show version
    show inventory
    show interfaces status
    show ip interface brief
    show vlan brief
    show interfaces trunk
    show spanning-tree summary
    show power inline
    show environment all
    show flash:
    show running-config

## Catalyst 2950SX Baseline Commands

    enable
    terminal length 0
    show version
    show interfaces status
    show vlan brief
    show interfaces trunk
    show spanning-tree summary
    show flash:
    show running-config

## Redaction Rules

Before committing command output to GitHub, redact:

- serial numbers
- full MAC addresses
- passwords
- public IP addresses
- private VPN addresses
- SSH keys
- SNMP community strings
- usernames if sensitive

## Storage

Baseline outputs should be saved under:

    configs/baseline/

Suggested filenames:

    3560cx-show-version.txt
    3560cx-show-inventory.txt
    3560cx-show-interfaces-status.txt
    3560cx-show-vlan-brief.txt
    2950sx-show-version.txt
    2950sx-show-interfaces-status.txt
    2950sx-show-vlan-brief.txt
