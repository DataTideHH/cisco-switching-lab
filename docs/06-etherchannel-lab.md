# EtherChannel Lab

## Goal

Bundle two physical links between the switches into one logical link.

This lab is optional and depends on available SFP modules, fiber cables and switch support.

## Possible Use Case

    2950SX uplink 1 + uplink 2
            |
            | EtherChannel / Port-Channel
            |
    3560CX SFP 1 + SFP 2

## Planned Verification Commands

    show etherchannel summary
    show interfaces trunk
    show spanning-tree
    show interfaces status

## Learning Goals

- understand physical vs logical links
- understand why EtherChannel avoids STP blocking for bundled links
- compare individual trunks with port-channel trunks
- practice LACP where supported
