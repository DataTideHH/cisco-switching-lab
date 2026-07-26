# Basic Switch Security

## Goal

Document practical, CCNA-level management hardening without publishing security-sensitive configuration details.

## Verified Management Baseline

The current Catalyst 3560CX baseline includes:

- SSH for normal remote administration
- serial console retained as an independent recovery path
- privileged local administrative access
- administrative secrets stored as Type 9 rather than legacy Type 5
- temporary SCP service disabled after the IOS transfer
- obsolete legacy SSH client exceptions removed after the IOS upgrade
- NTP configured so security and operational logs have useful timestamps
- configuration saved only after post-change validation

No credentials, password hashes, SSH keys or complete configuration exports are stored in this repository.

## Planned Hardening Topics

- dedicated management VLAN in the isolated lab
- separate unused native VLAN for lab trunks rather than using the management VLAN
- explicit management access restrictions
- unused ports assigned to a parking VLAN and shut down
- PortFast and BPDU Guard on verified end-device ports
- port security experiments on lab-only access ports
- DHCP snooping and Dynamic ARP Inspection concepts where supported
- centralized syslog and monitoring as future lab extensions

## Planned VLAN Role Separation

| VLAN | Security-oriented role |
|---:|---|
| 99 | management traffic |
| 998 | unused matching native VLAN on both ends of lab trunks; no SVI or end devices |
| 999 | parking VLAN for unused access ports; ports also shut down |

These roles should remain separate. An unused trunk native VLAN is not a substitute for the management VLAN, and a parking VLAN for shut down access ports is not used as the trunk native VLAN.

## Example: Parking Unused Ports

Interface ranges must be adapted to the real switch and must not include active uplinks or management paths.

```text
conf t

vlan 999
 name BLACKHOLE

interface range GigabitEthernet0/X - Y
 description UNUSED_LAB_PORT
 switchport mode access
 switchport access vlan 999
 shutdown

end
```

Do not save until the affected interfaces, uplinks and management access have been verified.

## Change-Safety Rules

Before changing management or access-control settings:

1. keep a console session available
2. identify the current management path
3. avoid changing all access methods at once
4. verify SSH in a second session before closing the first
5. confirm the boot path and saved configuration
6. verify native VLAN and allowed VLAN consistency on both ends of each trunk
7. redact all outputs before publication

## Documentation Rule

Publish the method and verification criteria, not secrets or full real configurations.