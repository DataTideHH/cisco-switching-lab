# Basic Switch Security

## Goal

Document basic CCNA-level switch hardening practices.

## Planned Topics

- set hostname
- disable unused ports
- assign unused ports to a parking VLAN
- configure management VLAN
- use SSH instead of Telnet where supported
- set secure passwords
- configure port security on access ports
- document DHCP snooping and Dynamic ARP Inspection concepts where supported

## Example: Parking Unused Ports

Interface ranges must be adapted to the real switch.

    conf t

    vlan 999
     name BLACKHOLE

    interface range FastEthernet0/2 - 24
     description UNUSED_PORT
     switchport mode access
     switchport access vlan 999
     shutdown

    end
    write memory

## Documentation Note

Do not publish real passwords or complete security-sensitive configurations.
