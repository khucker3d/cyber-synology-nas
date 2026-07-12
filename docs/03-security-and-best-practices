# Security and Best Practices

## Account Separation

Use separate accounts for separate functions.

| Account | Purpose |
|---|---|
| `nasadmin` | DSM administration |
| `nasuser` | Routine file access |
| Built-in `admin` | Disabled |
| Built-in `guest` | Disabled |

Administrative credentials should not be used for everyday SMB access.

## Network Placement

Place the NAS on a trusted internal network.

Do not place it on:

- Guest networks
- IoT networks
- Untrusted lab segments
- Directly exposed internet-facing networks

A future trusted-storage VLAN may be appropriate when firewall rules and access requirements are defined.

## Remote Access

Preferred approaches:

1. VPN for remote administration
2. QuickConnect for approved remote file access

Avoid:

- Direct DSM port forwarding
- Direct SMB port forwarding
- UPnP-created exposure
- Publishing remote-access identifiers

## SMB Baseline

```
Minimum protocol: SMB2
Maximum protocol: SMB3
SMB1: Disabled
Guest access: Disabled
```

Enable only the file-sharing services that are required.

## Storage Principles

- RAID is not backup.
- Synchronization is not backup.
- A configuration export is not a data backup.
- A backup should use separate storage.
- Critical files should also have an offline or offsite copy.
- Restore testing is required to prove a backup works.

## Operational Practices

- Keep DSM and packages updated.
- Review permissions after adding users or shares.
- Remove unused accounts and packages.
- Review drive health and storage alerts.
- Schedule maintenance during low-use windows.
- Store recovery codes outside the NAS.
- Store encryption passwords in a password manager.
- Document sanitized architecture publicly and retain sensitive details privately.

## Public Documentation Sanitization

Remove or replace:

- Real IP addresses
- Usernames
- Email addresses
- QuickConnect IDs
- MAC addresses
- Serial numbers
- Internal DNS names
- Screenshots showing personal files
- Authentication tokens and recovery codes
