# Verified Switch Baseline

## Purpose

A baseline captures the device state before and after changes. It supports troubleshooting, rollback decisions and reproducible documentation.

## Current Verified State

The Catalyst 3560CX baseline was checked after the IOS maintenance work:

- IOS `15.2(7)E14` booted successfully
- bootloader `15.2(7r)E` active
- primary and fallback boot images configured
- console and SSH access verified
- management SVI operational
- active links negotiated at 1 Gbit/s full duplex
- interface error counters showed no errors
- hardware POST completed successfully
- no relevant FAIL, ERROR or CRASH entries found in the checked logs
- NTP synchronization and CET/CEST clock settings verified

## Baseline Command Set

```text
enable
terminal length 0
show version
show inventory
show boot
show interfaces status
show interfaces counters errors
show ip interface brief
show vlan brief
show interfaces trunk
show spanning-tree summary
show power inline
show environment all
dir flash:
show logging
show clock detail
show ntp associations
show ntp status
```

## Change Validation Pattern

For disruptive changes, use this sequence:

1. capture the current state
2. verify available storage and image compatibility
3. verify file integrity
4. define a rollback or fallback path
5. keep console access available
6. perform the change
7. verify software, boot path, links, counters, logs and reachability
8. save the configuration only after validation

## Redaction Rules

Before publishing output, remove or replace:

- serial numbers
- full MAC addresses
- credentials and password hashes
- SSH keys
- real usernames where unnecessary
- public, private and VPN addresses
- hostnames and private interface descriptions
- complete raw configurations

Use synthetic values or concise statements of verified outcomes instead of publishing raw device dumps.