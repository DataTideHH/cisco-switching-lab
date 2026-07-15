# Lessons Learned

This document collects practical findings from the physical Cisco lab.

## IOS Maintenance

- A successful transfer does not prove image integrity; verify size and checksum.
- Define the fallback boot image before reloading.
- Keep serial console access available for disruptive maintenance.
- Observe image validation, bootloader changes, POST and interface recovery during boot.
- Remove temporary services and client-side compatibility exceptions after the maintenance window.

## SSH and SCP

- A modern OpenSSH client may require legacy compatibility settings when connecting to an older IOS release.
- After upgrading IOS, direct SSH should be retested before retaining those exceptions.
- Classic SCP mode may still be required with `scp -O` because the switch does not provide an SFTP subsystem.
- SSH and SCP compatibility are related but not identical checks.

## Credentials

- Legacy Type 5 secrets should be replaced when the platform supports stronger Type 9 storage.
- Never publish password hashes, even when they appear encrypted.
- Test the new login and privileged access in a separate session before closing the working session.

## NTP and DNS

- A hostname-based NTP server is unsuitable when DNS lookup is deliberately disabled and no resolver path is configured.
- A local router acting as NTP source gives the lab a simple, low-latency time hierarchy.
- Timezone and daylight-saving configuration remain necessary even after NTP synchronization.
- Accurate timestamps materially improve log correlation and troubleshooting.

## Topology and Risk Separation

- A wireless repeater operating as a bridge extends the same Layer 2 home LAN; it does not create a routed lab network.
- A future Cisco router should initially sit behind the existing home router and serve an isolated lab subnet.
- This limits DHCP, NAT, ACL, routing and IPv6 mistakes to the lab.
- STP loops and redundant links should be created only on dedicated lab ports.

## Portfolio Documentation

- Document verified outcomes rather than presenting planned hardware as already implemented.
- Keep the switching repository focused on device operation and Cisco CLI work.
- Keep data collection, Python, SQL, data quality and BI outputs in the related `network-operations-data-lab`.
- Publish sanitized methods and architecture, not the real home topology or raw configuration.