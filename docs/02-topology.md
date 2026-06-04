# Topology

## Initial Physical Topology

    Client / Test Device
            |
            | Access Port
            |
    Cisco Catalyst 2950SX-24
            |
            | 1000BASE-SX Fiber Trunk
            |
    Cisco Catalyst 3560CX-8PC-S
            |
            | Uplink / Management
            |
    Existing Lab or Home Network

## Logical VLAN Plan

| VLAN | Name | Purpose |
|---:|---|---|
| 10 | CLIENTS | test client devices |
| 20 | LAB | lab systems and experiments |
| 99 | MGMT | switch management |
| 999 | BLACKHOLE | unused ports / parking VLAN |

## Design Notes

The Catalyst 3560CX is planned as the central switch for management and possible Layer 3 functions.

The Catalyst 2950SX is planned as a legacy Layer 2 access switch.

The fiber link between both switches will be configured as an 802.1Q trunk.
