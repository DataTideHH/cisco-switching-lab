# VLAN and Trunk Lab

## Goal

Create a small, isolated VLAN design and carry selected VLANs across an 802.1Q trunk between two lab switches.

This is a planned multi-switch stage. It must use lab-only ports and must not alter the normal home LAN.

## Planned VLANs

| VLAN | Name | Purpose |
|---:|---|---|
| 10 | CLIENTS | test client devices |
| 20 | LAB | lab systems and experiments |
| 30 | SERVERS | test services and data systems |
| 99 | MGMT | switch management |
| 999 | BLACKHOLE | unused ports |

## Example Configuration Pattern

Exact interface names must be verified on each physical switch.

```text
conf t

vlan 10
 name CLIENTS
vlan 20
 name LAB
vlan 30
 name SERVERS
vlan 99
 name MGMT
vlan 999
 name BLACKHOLE

interface GigabitEthernet0/X
 description LAB_TRUNK_TO_SECOND_SWITCH
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,99
 no shutdown

end
copy running-config startup-config
```

The equivalent VLANs and trunk must be configured on the second switch.

## Access-Port Pattern

```text
interface GigabitEthernet0/Y
 description LAB_CLIENT
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 spanning-tree bpduguard enable
 no shutdown
```

PortFast and BPDU Guard are appropriate for verified end-device access ports, not for switch-to-switch trunks.

## Verification

```text
show vlan brief
show interfaces trunk
show interfaces status
show interfaces switchport
show spanning-tree vlan 10
show spanning-tree vlan 20
show spanning-tree vlan 30
show spanning-tree vlan 99
```

## Success Criteria

- expected VLANs exist on both switches
- only intended VLANs traverse the trunk
- access ports belong to the expected VLAN
- native VLAN configuration matches on both ends
- test clients communicate only as intended
- normal home-network connectivity remains unaffected

## Safety

Do not attach both ends of an unconfigured redundant link to the productive LAN. Redundant Layer 2 paths must be created only inside the isolated lab and observed through STP verification commands.