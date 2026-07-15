# Hardware Inventory

## Current Device

### Cisco Catalyst WS-C3560CX-8PC-S

Current role:

- compact managed switch in a private physical lab
- Cisco IOS and CCNA-oriented CLI practice platform
- Layer 2 switching and basic Layer 3 switching platform
- PoE-capable access switch for future lab expansion
- management and maintenance practice device

Verified public-safe baseline:

| Item | Verified value |
|---|---|
| Model | `WS-C3560CX-8PC-S` |
| IOS | `15.2(7)E14` |
| Bootloader | `15.2(7r)E` |
| License family | IP Base |
| Primary image | `c3560cx-universalk9-mz.152-7.E14.bin` |
| Fallback image | Previous `15.2(4)E4` image retained |
| Console access | USB-to-serial from macOS |
| Remote access | SSH |
| Time source | Local NTP source |
| Active link validation | 1 Gbit/s full duplex, counters checked |

The serial number, real hostname, management address, MAC addresses and private port descriptions are not published.

## Useful Baseline Commands

```text
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
show ntp associations
show ntp status
show clock detail
```

## Planned Expansion

The preferred next stage is:

- a second Catalyst 3560CX, ideally another `WS-C3560CX-8PC-S` or a lower-cost `WS-C3560CX-8TC-S`
- a used Cisco IOS or IOS XE router for routing, NAT, DHCP, ACL and WAN-edge labs
- copper trunks first; SFP links can be added later when they serve a specific learning goal

A legacy Catalyst 2950SX and a 1000BASE-SX fiber link remain optional ideas, not part of the current verified baseline.

## Selection Rationale

A second compatible switch adds more immediate CCNA value than replacing the current device with a new Catalyst 9200CX. It enables practical work with trunks, STP, EtherChannel and redundant Layer 2 paths while keeping cost and configuration differences manageable.