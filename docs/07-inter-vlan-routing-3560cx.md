# Inter-VLAN Routing on the Catalyst 3560CX

## Status

Planned isolated Layer 3 switching lab. No completed inter-VLAN routing result is claimed yet.

## Goal

Use the Catalyst 3560CX as a Layer 3 switch for basic routing between isolated lab VLANs and verify the result from both the switch and connected test clients.

## Prerequisites

- VLAN and trunk lab completed and verified
- console access available
- dedicated lab-only clients or test systems available in at least two VLANs
- current management path identified and excluded from accidental changes
- example subnets checked for overlap with the existing home network, VPNs and other lab networks
- rollback procedure documented before enabling routing

## Planned Addressing

Example only. Addresses must be checked and may be changed before implementation.

| VLAN | Example subnet | Example SVI | Purpose |
|---:|---|---|---|
| 10 | `192.168.10.0/24` | `192.168.10.1` | test clients |
| 20 | `192.168.20.0/24` | `192.168.20.1` | lab systems |
| 30 | `192.168.30.0/24` | `192.168.30.1` | test services |
| 99 | `192.168.99.0/24` | `192.168.99.1` | isolated lab management |

VLAN 998 remains the unused native VLAN for trunks and must not receive an SVI. VLAN 999 remains the parking VLAN for unused access ports.

## Initial Baseline

Capture before enabling routing:

```text
show vlan brief
show interfaces trunk
show ip interface brief
show ip route
show running-config | section interface Vlan
show running-config | include ^ip routing
show spanning-tree summary
```

Record the current management SVI and default-gateway behavior. Do not repurpose the existing home-network management path for this lab.

## Example Configuration Pattern

```text
conf t

interface vlan 10
 description CLIENTS_GATEWAY
 ip address 192.168.10.1 255.255.255.0
 no shutdown

interface vlan 20
 description LAB_GATEWAY
 ip address 192.168.20.1 255.255.255.0
 no shutdown

interface vlan 30
 description SERVERS_GATEWAY
 ip address 192.168.30.1 255.255.255.0
 no shutdown

interface vlan 99
 description MGMT_GATEWAY
 ip address 192.168.99.1 255.255.255.0
 no shutdown

ip routing

end
```

An SVI becomes operational only when its VLAN exists and at least one associated Layer 2 port or trunk path is active.

The example management SVI is for the future isolated lab design. It must not replace a working management address until console recovery and the new path have been tested.

## Test-Client Configuration

Each test client needs:

- an address in its assigned VLAN subnet
- the corresponding SVI as its default gateway
- a lab-only switch access port in the expected VLAN

Example:

```text
VLAN 10 client: 192.168.10.10/24, gateway 192.168.10.1
VLAN 20 client: 192.168.20.10/24, gateway 192.168.20.1
```

## Verification

Switch-side checks:

```text
show ip interface brief
show interfaces vlan 10
show interfaces vlan 20
show interfaces vlan 30
show interfaces vlan 99
show ip route
show ip route connected
show vlan brief
show interfaces trunk
show arp
show interfaces counters errors
show logging
```

Basic SVI checks:

```text
ping 192.168.10.1
ping 192.168.20.1
ping 192.168.30.1
ping 192.168.99.1
```

Pinging the switch's own SVI addresses is not sufficient evidence of inter-VLAN routing. Test from connected clients:

1. ping each client's own default gateway
2. ping a client in another routed VLAN
3. confirm the expected connected route exists on the switch
4. verify the ARP table contains the test endpoints
5. confirm that non-routed or intentionally excluded VLANs remain unreachable

## Learning Goals

- understand switched virtual interfaces
- understand default gateways for VLANs
- distinguish Layer 2 switching from Layer 3 switching
- recognize connected routes created by active SVIs
- validate routing from actual endpoints rather than only from the switch
- prepare for later ACL tests between management, client and service VLANs

## Success Criteria

- intended SVIs are operational
- connected routes appear for each active routed VLAN
- each client reaches its own SVI
- clients in different routed VLANs communicate only as intended
- VLAN 998 has no SVI and carries no endpoint traffic
- VLAN 999 remains an unused-port parking VLAN
- management remains reachable through the planned recovery path
- interface counters and logs show no unexplained errors
- the productive home network remains unaffected

## Rollback

1. keep console access active
2. disconnect lab clients if unexpected routing occurs
3. disable `ip routing` if Layer 3 forwarding must be stopped immediately
4. shut down or remove only the newly introduced lab SVIs after checking dependencies
5. restore the recorded management and gateway baseline
6. verify VLAN, trunk and management state before saving

Do not remove or alter an existing management SVI without a tested alternative access path.

## Evidence to Record

Publish only sanitized evidence:

- planned subnet and VLAN table
- connected-route summary
- client-to-gateway and inter-VLAN test matrix
- expected versus observed result
- rollback test or recovery-path confirmation
- addresses generalized or replaced where publication could expose the real topology

## Safety

Perform routing tests only inside the isolated lab. Do not enable DHCP, NAT, default routes or dynamic routing as part of this basic SVI exercise.