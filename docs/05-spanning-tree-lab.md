# Spanning Tree Lab

## Status

Planned multi-switch lab. No completed STP experiment is claimed yet.

## Goal

Observe how Spanning Tree Protocol prevents Layer 2 loops when redundant links exist between two isolated lab switches.

## Prerequisites

- two managed switches available
- console access to both switches
- VLAN and single-trunk baseline already verified
- dedicated lab-only inter-switch ports identified
- productive home-network uplinks excluded from the experiment
- current STP mode and root bridge recorded before changes

## Initial Baseline

With only one verified trunk between the switches, capture:

```text
show spanning-tree summary
show spanning-tree root
show spanning-tree vlan 10
show spanning-tree vlan 20
show spanning-tree vlan 30
show spanning-tree vlan 99
show spanning-tree vlan 998
show interfaces trunk
show interfaces status
```

Record:

- current STP mode
- root bridge for each lab VLAN
- root and designated ports
- trunk interfaces and allowed VLANs
- interface counters before the experiment

Do not change the STP mode merely to match an example. First observe the mode already supported and configured on the physical switches.

## Planned Scenario

1. start with one working trunk between the switches
2. verify VLAN, native VLAN and STP state on both ends
3. connect a second lab-only physical link between the switches
4. observe which link remains forwarding and which port becomes an alternate or blocking path
5. disconnect the active path and observe reconvergence through the remaining link
6. restore the original single-link topology

The second link must use a compatible trunk configuration, including the same native VLAN and allowed VLAN list:

```text
switchport mode trunk
switchport trunk native vlan 998
switchport trunk allowed vlan 10,20,30,99,998
```

## Verification Commands

```text
show spanning-tree
show spanning-tree summary
show spanning-tree root
show spanning-tree vlan 10
show spanning-tree vlan 20
show spanning-tree vlan 30
show spanning-tree vlan 99
show spanning-tree vlan 998
show interfaces trunk
show interfaces status
show interfaces counters errors
show logging
```

## Learning Goals

- understand root bridge election
- identify root, designated and alternate ports
- distinguish forwarding and discarding or blocking states
- observe how redundant Layer 2 paths are controlled
- understand why unmanaged Layer 2 loops are dangerous
- compare normal convergence with link-failure reconvergence
- relate STP state to VLAN and trunk configuration

## Success Criteria

- the root bridge is identified for each tested VLAN
- one redundant path is prevented from forwarding user traffic
- no broadcast storm or uncontrolled loop occurs
- the remaining path forwards after the active path is disconnected
- VLAN 998 remains the matching unused native VLAN on both trunks
- interface counters and logs show no unexplained errors
- the productive home network remains unaffected

## Rollback

1. disconnect the second redundant link
2. return the affected interfaces to the recorded single-trunk baseline
3. verify the original trunk and STP state
4. confirm normal management reachability
5. save only if the restored state is verified and intentionally retained

Keep console access available throughout the experiment.

## Evidence to Record

Publish only sanitized evidence:

- root bridge and port-role summaries
- forwarding and alternate-port observations
- a small before/failure/after table
- approximate reconvergence observations without exposing private topology
- unexpected behavior and the corrective step taken

## Safety Note

Do not create unmanaged Layer 2 loops in the existing home network. Add redundant paths only on isolated lab ports after the first trunk has been verified and while console recovery is available.