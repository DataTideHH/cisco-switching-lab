# IOS Upgrade Workflow

## Scope

This document records the verified maintenance method used for a Cisco Catalyst 3560CX. It intentionally excludes credentials, real addresses, hostnames and local private file paths.

## Verified Upgrade

| Item | Previous | Current |
|---|---|---|
| Cisco IOS | `15.2(4)E4` | `15.2(7)E14` |
| Bootloader | `15.2(4r)E3` | `15.2(7r)E` |
| Platform | `WS-C3560CX-8PC-S` | unchanged |

The previous IOS image was retained as a fallback.

## Preparation

Before transferring an image:

```text
show version
show boot
dir flash:
show environment all
show logging
```

Confirm:

- exact platform and image family
- sufficient flash capacity
- console access is available
- current configuration is saved
- official checksum information is available
- the previous bootable image remains accessible

## Integrity Chain

The maintenance workflow used two integrity checks:

1. verify the downloaded file locally against the vendor-published checksum
2. verify the copied image again on the switch flash

Example switch-side verification:

```text
verify /md5 flash:/IMAGE_FILENAME.bin
```

A successful file transfer is not sufficient evidence that the file is correct; size and checksum should both be checked.

## Transfer

The image was copied over SCP after temporarily enabling the SCP server on the switch. Older Cisco IOS releases may require classic SCP protocol mode from a modern OpenSSH client:

```text
scp -O IMAGE_FILENAME.bin SWITCH_ALIAS:IMAGE_FILENAME.bin
```

The `-O` option selects the legacy SCP protocol instead of SFTP. It should be used only when required by the target device.

After transfer, disable the temporary SCP service again when it is not needed.

## Boot Path and Fallback

Configure the new image as primary and retain the known bootable previous image as fallback.

Conceptual example:

```text
no boot system
boot system flash:/NEW_IMAGE.bin;flash:/OLD_IMAGE.bin
```

Verify the result before reloading:

```text
show boot
```

The exact syntax and paths must be checked for the installed IOS release and flash layout.

## Reload and Console Observation

A serial console was kept open during the reload. This allowed observation of:

- image signature validation
- bootloader update
- microcode update
- hardware POST
- IOS initialization

Console access is the recovery path if SSH or management addressing fails after the change.

## Post-Upgrade Validation

```text
show version
show boot
show interfaces status
show interfaces counters errors
show ip interface brief
show environment all
show logging
show clock detail
show ntp status
```

Validate:

- expected IOS and bootloader versions
- expected primary and fallback paths
- active interfaces and negotiated speed/duplex
- interface errors
- hardware environment
- relevant log errors
- management reachability
- SSH access
- time synchronization

## Security Follow-Up

After the software upgrade:

- legacy administrative secrets were replaced with Type 9 secrets
- temporary SCP service was disabled
- obsolete client-side legacy SSH algorithm exceptions were removed after direct SSH testing succeeded
- the configuration was saved after validation

## Lessons

- define rollback before reload
- verify an image both before and after transfer
- keep the previous image until the new release is proven stable
- use console access for disruptive maintenance
- do not publish raw configurations or password hashes
- treat maintenance as a controlled change, not merely a file copy and reboot