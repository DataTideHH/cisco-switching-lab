# EtherChannel Lab

## Goal

Bundle two physical links between two lab switches into one logical Port-Channel and compare the result with separate redundant trunks.

## Planned Topology

```text
Catalyst 3560CX-1
   Gi0/X ===== Gi0/X
   Gi0/Y ===== Gi0/Y
          LACP
Catalyst 3560CX-2
```

Copper links are preferred for the first implementation because they reduce cost and remove unnecessary SFP and fiber variables.

## Example LACP Pattern

Exact interfaces must be verified before configuration.

```text
interface range GigabitEthernet0/X - Y
 description LAB_LACP_MEMBERS
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,99
 channel-group 1 mode active
 no shutdown

interface Port-channel1
 description LAB_TRUNK_TO_SECOND_SWITCH
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,99
```

Apply a compatible configuration on the second switch.

## Verification

```text
show etherchannel summary
show interfaces port-channel 1
show interfaces trunk
show spanning-tree
show interfaces counters errors
```

## Learning Goals

- distinguish physical member links from a logical Port-Channel
- understand LACP active and passive modes
- recognize configuration consistency requirements
- understand why STP treats the bundle as one logical path
- troubleshoot suspended or misconfigured members

## Safety

Build and verify the Port-Channel on isolated lab ports. Do not connect a second parallel link to the productive LAN before STP or EtherChannel behavior is understood and checked.