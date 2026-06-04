# Inter-VLAN Routing on the Catalyst 3560CX

## Goal

Use the Catalyst 3560CX as a Layer 3 switch for basic inter-VLAN routing.

## Planned VLAN Interfaces

Example only. IP addresses may be changed later.

    interface vlan 10
     description CLIENTS_Gateway
     ip address 192.168.10.1 255.255.255.0
     no shutdown

    interface vlan 20
     description LAB_Gateway
     ip address 192.168.20.1 255.255.255.0
     no shutdown

    interface vlan 99
     description MGMT_Gateway
     ip address 192.168.99.1 255.255.255.0
     no shutdown

    ip routing

## Verification

    show ip interface brief
    show ip route
    show vlan brief
    ping 192.168.10.1
    ping 192.168.20.1
    ping 192.168.99.1

## Learning Goals

- understand SVIs
- understand default gateways for VLANs
- understand basic routing between VLANs
- distinguish Layer 2 switching from Layer 3 switching
