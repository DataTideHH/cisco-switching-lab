# Hardware Inventory

## Cisco Catalyst 3560CX-8PC-S

Planned role:

- compact core / distribution switch for the lab
- Layer 3-capable switch for basic inter-VLAN routing
- PoE-capable switch for possible future access point or VoIP tests
- SFP endpoint for the fiber trunk to the Catalyst 2950SX

Planned baseline commands:

    show version
    show inventory
    show interfaces status
    show ip interface brief
    show vlan brief
    show power inline
    show environment all
    show flash:
    show running-config

Values to document after inspection:

    Model: WS-C3560CX-8PC-S
    Serial: REDACTED
    IOS version: TBD
    License / image: TBD
    Uptime: TBD
    SFP module detected: TBD
    PoE status: TBD

## Cisco Catalyst WS-C2950SX-24

Planned role:

- legacy Layer 2 access switch
- access ports for test clients
- 1000BASE-SX fiber uplink to the Catalyst 3560CX
- VLAN, trunking and STP practice

Planned baseline commands:

    show version
    show interfaces status
    show vlan brief
    show interfaces trunk
    show spanning-tree
    show running-config

Values to document after inspection:

    Model: WS-C2950SX-24
    Serial: REDACTED
    IOS version: TBD
    Image: TBD
    Uptime: TBD
    1000BASE-SX uplink status: TBD

## Fiber Link

Planned connection:

    Catalyst 2950SX fixed 1000BASE-SX uplink
    -> MT-RJ to LC multimode fiber cable
    -> 1000BASE-SX SFP module
    -> Catalyst 3560CX SFP slot

Planned parts:

    SFP: Cisco-compatible GLC-SX-MMD or equivalent
    Cable: MT-RJ to LC duplex multimode, OM2 or OM3
