# Topology

## Current Public-Safe Physical Baseline

```text
Local router / time source
        )) wireless bridge / repeater ((
                         |
                         | Ethernet uplink
                         |
              Cisco Catalyst 3560CX
                         |
                         | access link
                         |
                   local client
```

This is a sanitized representation. Real addresses, hostnames, port numbers and private topology details are intentionally omitted.

The wireless bridge/repeater extends the existing home LAN at Layer 2. It does not create a separate routed subnet for the switch.

## Planned Lab Expansion

```text
Existing home LAN
        |
        | router outside / WAN side
        |
   Cisco lab router
        |
        | isolated lab networks
        |
   Catalyst 3560CX-1 ===== Catalyst 3560CX-2
              redundant trunk or EtherChannel
```

The Cisco router should initially operate as an additional isolated lab gateway behind the existing home router. This limits the impact of mistakes involving NAT, DHCP, ACLs, routing or IPv6.

## Planned Logical Segmentation

| VLAN | Example name | Purpose |
|---:|---|---|
| 10 | CLIENTS | test client devices |
| 20 | LAB | lab services and experiments |
| 30 | SERVERS | data and application services |
| 99 | MGMT | device management |
| 999 | BLACKHOLE | unused ports |

These VLANs are a roadmap, not a claim about the current productive home LAN.

## Design Principles

- keep experimental routing separate from the normal home gateway
- use dedicated lab-only ports for loop and STP experiments
- begin with copper links before adding fiber complexity
- retain console access as an independent recovery path
- document verification and rollback before each disruptive change
- publish only sanitized topology information