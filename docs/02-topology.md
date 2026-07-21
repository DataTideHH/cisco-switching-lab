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
        |
        | staged access link or later 802.1Q trunk
        |
   future dedicated Proxmox host
        |
        | virtual bridges and isolated lab guests
        |
   test VMs / LXC containers
```

The Cisco router should initially operate as an additional isolated lab gateway behind the existing home router. This limits the impact of mistakes involving NAT, DHCP, ACLs, routing or IPv6.

The Proxmox host shown here is a future design target only. No dedicated x86 host has been acquired and no Proxmox installation is currently claimed.

## Planned Logical Segmentation

| VLAN | Example name | Purpose |
|---:|---|---|
| 10 | CLIENTS | test client devices |
| 20 | LAB | lab services and experiments |
| 30 | SERVERS | data, application and future virtualization services |
| 99 | MGMT | network and future hypervisor management |
| 999 | BLACKHOLE | unused ports |

These VLANs are a roadmap, not a claim about the current productive home LAN.

A future Proxmox integration should begin conservatively with one access VLAN. VLAN-aware bridges and an 802.1Q trunk should only be added after the basic host installation, console recovery path and switch rollback procedure have been validated.

## Repository Boundaries

- physical switch configuration, VLANs, trunks and reachability tests belong in `cisco-switching-lab`
- hypervisor installation, virtual bridges, VM and LXC lifecycle, storage and backup belong in the planned `proxmox-virtualization-lab`
- sanitized infrastructure inventory, API exports, data-quality checks and BI outputs belong in `network-operations-data-lab`

## Design Principles

- keep experimental routing separate from the normal home gateway
- use dedicated lab-only ports for loop and STP experiments
- begin with copper links before adding fiber complexity
- retain console access as an independent recovery path
- connect a future virtualization host through a simple access port before testing trunks
- separate management traffic from guest and service traffic when the lab reaches that stage
- document verification and rollback before each disruptive change
- publish only sanitized topology information