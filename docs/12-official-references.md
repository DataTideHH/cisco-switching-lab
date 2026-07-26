# Official References and Learning Resources

## Purpose

This document collects the primary references used to plan, verify and document the Cisco switching lab.

The repository remains a practical lab record rather than a mirror of vendor documentation. Dynamic documentation is linked directly so that the current official version remains the source of truth.

## Cisco Catalyst 3560-CX Platform References

- [Cisco Catalyst 3560-CX support page](https://www.cisco.com/c/en/us/support/switches/catalyst-3560-cx-series-switches/series.html)
- [Consolidated Platform Configuration Guide, Cisco IOS Release 15.2(7)Ex](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst2960cx_3650cx/software/release/15-2_7_e/configuration_guide/b_1527e_consolidated_3560cx_2960cx_cg.html)
- [Configuring VLANs](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst2960cx_3650cx/software/release/15-2_7_e/configuration_guide/b_1527e_consolidated_3560cx_2960cx_cg/m_vlan_vlan_cg_2960-x.html)
- [Configuring VLAN Trunks](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst2960cx_3650cx/software/release/15-2_7_e/configuration_guide/b_1527e_consolidated_3560cx_2960cx_cg/configuring_vlan_trunks.html)
- [Release notes for Catalyst 3560-CX and 2960-CX, Cisco IOS 15.2(7)E](https://www.cisco.com/c/en/us/support/switches/catalyst-3560-cx-series-switches/products-release-notes-list.html)
- [End-of-Sale and End-of-Life announcement for selected Catalyst 3560-CX models](https://www.cisco.com/c/en/us/products/collateral/switches/catalyst-3560-cx-series-switches/catalyst-3560-cx-serie-switche-eol.html)

## Curated DataTideHH Learning References

The related [`open-learning-resources`](https://github.com/DataTideHH/open-learning-resources) repository provides license-aware, link-only reference entries for:

- [Catalyst 3560-CX IOS 15.2E documentation](https://github.com/DataTideHH/open-learning-resources/tree/main/resources/networking/cisco-catalyst-3560cx-ios-15-2e-reference)
- [Cisco Networking Academy and Packet Tracer](https://github.com/DataTideHH/open-learning-resources/tree/main/resources/networking/cisco-networking-academy-packet-tracer)
- [Core Internet standards and the RFC Editor](https://github.com/DataTideHH/open-learning-resources/tree/main/resources/networking/core-internet-standards-rfc-editor)

## Usage Rules

Before applying an example configuration:

1. verify the exact switch model, license and IOS release
2. check feature support and release-specific caveats
3. capture the current state and define a rollback path
4. adapt interface names and VLAN IDs to the isolated lab only
5. keep console access available for disruptive changes
6. validate the result before saving the configuration
7. publish only sanitized commands, methods and outcomes

Vendor documentation and release notes take precedence over examples in this learning repository.