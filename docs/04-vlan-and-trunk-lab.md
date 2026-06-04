# VLAN and Trunk Lab

## Goal

Create a basic VLAN design and carry multiple VLANs over the fiber trunk between the Catalyst 2950SX and the Catalyst 3560CX.

## Planned VLANs

| VLAN | Name | Purpose |
|---:|---|---|
| 10 | CLIENTS | regular test clients |
| 20 | LAB | lab systems |
| 99 | MGMT | switch management |
| 999 | BLACKHOLE | unused ports |

## Example Configuration: Catalyst 3560CX

Interface names must be verified on the real device before use.

    conf t

    vlan 10
     name CLIENTS
    vlan 20
     name LAB
    vlan 99
     name MGMT
    vlan 999
     name BLACKHOLE

    interface GigabitEthernet1/0/X
     description TRUNK_to_2950SX
     switchport mode trunk
     switchport trunk native vlan 99
     switchport trunk allowed vlan 10,20,99
     no shutdown

    end
    write memory

## Example Configuration: Catalyst 2950SX

Interface names must be verified on the real device before use.

    conf t

    vlan 10
     name CLIENTS
    vlan 20
     name LAB
    vlan 99
     name MGMT
    vlan 999
     name BLACKHOLE

    interface GigabitEthernet0/X
     description TRUNK_to_3560CX
     switchport mode trunk
     switchport trunk native vlan 99
     switchport trunk allowed vlan 10,20,99
     no shutdown

    end
    write memory

## Verification

    show vlan brief
    show interfaces trunk
    show interfaces status
    show spanning-tree vlan 10
    show spanning-tree vlan 20
    show spanning-tree vlan 99

## Notes

The exact interface names may differ between switch models and IOS versions.
