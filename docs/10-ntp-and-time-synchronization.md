# NTP and Time Synchronization

## Goal

Use a stable local time source for the Cisco switch so that logs and troubleshooting timestamps are consistent with the rest of the local environment.

## Public-Safe Architecture

```text
External time source
        |
        v
Local router / NTP server
        |
        +---- Cisco Catalyst switch
        |
        +---- macOS client
```

The real addresses and device names are intentionally omitted.

## Why a Local Time Source

Using the local router as the immediate NTP source provides:

- one consistent clock source for local devices
- low-latency synchronization inside the LAN
- fewer direct external dependencies on the switch
- simpler troubleshooting
- meaningful timestamps in logs after reloads

## Cisco IOS Configuration Pattern

```text
clock timezone CET 1 0
clock summer-time CEST recurring last Sun Mar 2:00 last Sun Oct 3:00
ntp server LOCAL_NTP_ADDRESS prefer
```

The address must be replaced with the actual local NTP source in the private configuration.

A hostname-based NTP configuration was avoided because DNS lookup was intentionally disabled on the switch. Using an unresolved hostname while `no ip domain-lookup` is active can lead to repeated translation attempts and failed synchronization.

## Verification

```text
show clock detail
show ntp associations
show ntp status
```

A healthy result should show:

- the clock source as NTP
- the selected peer marked as synchronized
- the expected local timezone
- correct daylight-saving transition information
- a stable stratum relationship

## Verified Outcome

The current switch successfully synchronized to the local NTP source. The local router operated as the upstream peer, while the switch became one stratum level lower in the hierarchy.

## Operational Relevance

Accurate time supports:

- correlation of interface events and log messages
- comparison of switch events with client-side observations
- maintenance records
- troubleshooting sequences
- future syslog, monitoring and operational-data workflows

This is also relevant to the related `network-operations-data-lab`, where timestamps are part of reliable operational data.