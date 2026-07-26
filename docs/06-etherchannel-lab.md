# EtherChannel Lab

## Status

Planned multi-switch lab. No completed EtherChannel result is claimed yet.

## Goal

Bundle two physical links between two isolated lab switches into one logical Port-Channel using LACP and compare the result with separate redundant trunks controlled by STP.

## Prerequisites

- two compatible managed switches available
- console access to both switches
- VLAN and single-trunk baseline already verified
- two matching lab-only interfaces available on each switch
- interface speed, duplex and switchport characteristics verified
- current configurations and interface states recorded

## Planned Topology

```text
Catalyst 3560CX-1
   Gi0/X ===== Gi0/X
   Gi0/Y ===== Gi0/Y
          LACP
Catalyst 3560CX-2
```

Copper links are preferred for the first implementation because they reduce cost and remove unnecessary SFP and fiber variables.

## Initial Baseline

Before creating the channel, capture on both switches:

```text
show interfaces status
show interfaces trunk
show interfaces switchport
show spanning-tree summary
show etherchannel summary
show interfaces counters errors
show running-config | section interface
```

Verify that both candidate interfaces are dedicated to the isolated lab and are not part of an existing channel.

## Change Plan

1. verify matching interface characteristics on both switches
2. configure LACP active mode on the intended member links
3. configure the logical Port-Channel as the trunk
4. use VLAN 998 as the matching unused native VLAN
5. allow only VLANs 10, 20, 30, 99 and 998
6. verify that all members bundle successfully
7. test one-member failure and recovery
8. save only after validation

## Example LACP Pattern

Exact interfaces and command order must be verified for the installed IOS release.

```text
conf t

interface range GigabitEthernet0/X - Y
 description LAB_LACP_MEMBER
 channel-group 1 mode active
 no shutdown

interface Port-channel1
 description LAB_TRUNK_TO_SECOND_SWITCH
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 10,20,30,99,998
 no shutdown

end
```

Apply a compatible configuration on the second switch. Member interfaces must have matching Layer 2 characteristics, and the Port-Channel trunk configuration must match on both ends.

VLAN 998 should have no SVI and no connected end devices. Management remains in VLAN 99.

## Verification

```text
show etherchannel summary
show etherchannel port-channel
show interfaces port-channel 1
show interfaces trunk
show interfaces switchport
show spanning-tree
show interfaces counters errors
show logging
```

For the failure test:

1. confirm the Port-Channel is forwarding normally
2. disconnect one physical member
3. verify that the logical Port-Channel remains operational through the other member
4. reconnect the member
5. verify that it rejoins the bundle without errors

## Learning Goals

- distinguish physical member links from a logical Port-Channel
- understand LACP active and passive modes
- recognize configuration consistency requirements
- understand why STP treats the bundle as one logical path
- troubleshoot suspended or misconfigured members
- observe resilience when one physical member fails

## Success Criteria

- both intended physical interfaces join the same logical Port-Channel
- no member is suspended or standalone unexpectedly
- the Port-Channel appears as one logical STP path
- the allowed VLAN list and native VLAN match on both ends
- VLAN 998 remains unused except as the trunk native VLAN
- traffic continues when one member link is disconnected
- the recovered member rejoins cleanly
- interface counters and logs show no unexplained errors
- the productive home network remains unaffected

## Rollback

1. disconnect one member so only a single known path remains
2. remove the channel-group association only from the dedicated lab member interfaces
3. restore the recorded single-trunk or disconnected baseline
4. verify STP, trunk and management state
5. save only after the restored state is confirmed

Do not use broad interface cleanup commands without first comparing the affected ports with the recorded baseline.

## Evidence to Record

Publish only sanitized evidence:

- `show etherchannel summary` state with private descriptions removed
- Port-Channel and member status before, during and after a one-link failure
- allowed VLAN and native VLAN verification
- any consistency error and how it was corrected
- confirmation that no productive uplink was involved

## Safety

Build and verify the Port-Channel only on isolated lab ports. Do not connect a second parallel link to the productive LAN before STP and EtherChannel behavior are understood and checked.