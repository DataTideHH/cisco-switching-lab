# CCNA Switching Cheatsheet

## Basic Show Commands

    show version
    show inventory
    show interfaces status
    show ip interface brief
    show vlan brief
    show interfaces trunk
    show spanning-tree
    show mac address-table
    show running-config

## VLANs

    conf t
    vlan 10
     name CLIENTS
    end
    show vlan brief

## Access Port

    conf t
    interface FastEthernet0/1
     switchport mode access
     switchport access vlan 10
     no shutdown
    end

## Trunk Port

    conf t
    interface GigabitEthernet0/1
     switchport mode trunk
     switchport trunk native vlan 99
     switchport trunk allowed vlan 10,20,99
     no shutdown
    end

## Save Configuration

    write memory

or:

    copy running-config startup-config

## STP

    show spanning-tree
    show spanning-tree vlan 10
    show spanning-tree summary

## EtherChannel

    show etherchannel summary
    show interfaces port-channel

## Troubleshooting Order

1. Physical link up?
2. Correct cable / SFP?
3. Interface not shutdown?
4. Same speed / duplex?
5. VLAN exists?
6. Access VLAN correct?
7. Trunk allowed VLAN correct?
8. Native VLAN mismatch?
9. STP blocking?
10. IP addressing correct?
