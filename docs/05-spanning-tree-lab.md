# Spanning Tree Lab

## Goal

Observe how Spanning Tree Protocol prevents Layer 2 loops when redundant links exist between switches.

## Simple STP Scenario

Start with one trunk link between the switches.

Then add a second physical link between the switches and observe which port is forwarding and which port is blocking.

## Verification Commands

    show spanning-tree
    show spanning-tree summary
    show spanning-tree vlan 10
    show spanning-tree vlan 20
    show spanning-tree vlan 99
    show interfaces status

## Learning Goals

- understand root bridge election
- identify root ports and designated ports
- observe blocking / forwarding states
- understand why Layer 2 loops are dangerous
- compare a single trunk link with redundant links

## Safety Note

Do not create unmanaged Layer 2 loops in the existing home network.
