# VLAN and Trunk Lab

## Status

Planned multi-switch lab. No completed result is claimed yet.

## Goal

Create a small, isolated VLAN design and carry selected VLANs across an 802.1Q trunk between two lab switches.

The lab must use dedicated lab-only ports and must not alter the normal home LAN.

## Prerequisites

- second compatible managed switch available
- console access to both switches
- current configurations backed up or recorded
- exact interface names verified on both devices
- one known working management and recovery path retained
- only one physical inter-switch link connected during the initial trunk setup

## Planned VLANs

| VLAN | Name | Purpose |
|---:|---|---|
| 10 | CLIENTS | test client devices |
| 20 | LAB | lab systems and experiments |
| 30 | SERVERS | test services and data systems |
| 99 | MGMT | switch management |
| 998 | NATIVE-UNUSED | unused native VLAN for lab trunks |
| 999 | BLACKHOLE | unused access ports, shut down |

VLAN 998 is not a management VLAN and should not have an SVI or connected end devices. VLAN 999 is reserved for unused access ports and is not the trunk native VLAN.

## Initial Baseline

Capture the current state on both switches before configuration:

```text
show version
show vlan brief
show interfaces status
show interfaces trunk
show interfaces switchport
show spanning-tree summary
show running-config | section interface
```

Record which interfaces are unused and dedicated to the lab. Do not use the productive uplink or current management path.

## Change Plan

1. create the same VLAN definitions on both switches
2. configure one lab-only inter-switch link as a static trunk on both ends
3. assign VLAN 998 as the matching native VLAN on both ends
4. allow only VLANs 10, 20, 30, 99 and 998
5. validate the trunk before adding access ports
6. configure one or more lab-only access ports
7. test intended Layer 2 connectivity
8. save only after verification

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
vlan 998
 name NATIVE_UNUSED
vlan 999
 name BLACKHOLE

interface GigabitEthernet0/X
 description LAB_TRUNK_TO_SECOND_SWITCH
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 10,20,30,99,998
 no shutdown

end
```

Apply a matching trunk configuration on the second switch. The native VLAN and allowed VLAN list must match on both ends.

Do not save the configuration until the trunk and recovery path have been verified.

## Access-Port Pattern

```text
conf t

interface GigabitEthernet0/Y
 description LAB_CLIENT
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 spanning-tree bpduguard enable
 no shutdown

end
```

PortFast and BPDU Guard are appropriate for verified end-device access ports, not for switch-to-switch trunks.

## Unused-Port Pattern

Interface ranges must be adapted carefully so active uplinks, trunks and management ports are excluded.

```text
conf t

interface range GigabitEthernet0/A - B
 description UNUSED_LAB_PORT
 switchport mode access
 switchport access vlan 999
 shutdown

end
```

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
show spanning-tree vlan 998
show interfaces counters errors
```

Where test clients are available, verify:

- same-VLAN communication across the trunk
- isolation from VLANs that are not routed
- expected access-port VLAN membership
- continued access through the independent management or console path

## Success Criteria

- expected VLANs exist on both switches
- only intended VLANs traverse the trunk
- VLAN 998 is the matching native VLAN on both ends
- VLAN 998 has no SVI and no connected end devices
- management remains in VLAN 99 rather than the native VLAN
- access ports belong to the expected VLAN
- unused lab ports are in VLAN 999 and shut down
- interface counters show no unexpected errors
- normal home-network connectivity remains unaffected

## Rollback

Before saving:

1. disconnect any newly added redundant link
2. restore the affected lab interfaces to their recorded initial state
3. remove only the newly created lab VLANs when they are no longer referenced
4. verify the original management and uplink path
5. compare the result with the captured baseline

If the management path is lost, use the retained console session rather than making additional remote changes blindly.

## Evidence to Record

Publish only sanitized evidence:

- VLAN and trunk summaries with addresses, hostnames and port descriptions redacted
- a concise before/after table
- success criteria and observed results
- any mismatch found and how it was corrected
- confirmation that the productive home LAN was unaffected

## Safety

Do not attach both ends of an unconfigured redundant link to the productive LAN. Redundant Layer 2 paths must be created only inside the isolated lab and observed through STP verification commands.