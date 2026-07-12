# Synology NAS Personal Cloud

![Status](https://img.shields.io/badge/status-operational-success)
![Platform](https://img.shields.io/badge/platform-Synology%20DSM-blue)
![Storage](https://img.shields.io/badge/storage-SHR-informational)
![Access](https://img.shields.io/badge/access-SMB%20%7C%20QuickConnect-lightgrey)
![Documentation](https://img.shields.io/badge/documentation-complete-success)

A secure, cross-platform personal cloud and shared-storage deployment built with a two-bay Synology NAS, a NAS-rated hard drive, and a managed home network.

This project demonstrates storage deployment, network integration, account hardening, SMB configuration, remote access, health monitoring, configuration backup, and recovery planning.

> All hostnames, IP addresses, usernames, remote-access identifiers, and topology details in this public repository are sanitized examples.

## Project Goals

- Create a local alternative to consumer cloud storage
- Provide shared file access for Windows and macOS
- Support secure mobile and remote access
- Separate administrative and everyday user accounts
- Use modern SMB protocols
- Monitor drive and storage health
- Maintain configuration backups
- Prepare for versioned data backups and restore testing
- Keep personal storage separate from cybersecurity lab systems

## Architecture

```text
Internet
   |
ISP Gateway
   |
Managed Security Gateway
   |
Managed Switch
   |
   +-- Synology NAS
   |     Hostname: nas-storage-01
   |     IP: 192.168.50.30
   |
   +-- Network Utility Server
   |     IP: 192.168.50.25
   |
   +-- Management Controller
   |     IP: 192.168.50.3
   |
   +-- Windows Workstation
   |
   +-- macOS Workstation
```

## Environment

| Component | Sanitized example |
|---|---|
| NAS | Two-bay Synology NAS |
| Internal drive | 4 TB NAS-rated SATA HDD |
| Storage pool | Synology Hybrid RAID |
| Volume | Single DSM volume |
| Network | Managed trusted LAN |
| NAS hostname | `nas-storage-01` |
| NAS address | `192.168.50.30` |
| Administrator | `nasadmin` |
| Standard user | `nasuser` |
| Shared folder | `Personal` |

## Implemented Controls

- Reserved DHCP address
- Separate administrator and standard accounts
- Administrator multi-factor authentication
- Built-in administrator disabled
- Guest account disabled
- Auto Block and Account Protection
- SMB1 disabled
- SMB2 minimum and SMB3 maximum
- No direct SMB or DSM port forwarding
- Secure remote access through QuickConnect
- Scheduled S.M.A.R.T. testing
- Scheduled data scrubbing
- Email notifications
- Manual and automatic DSM configuration backup
- Minimal package footprint

## Validation

| Test | Result |
|---|---|
| NAS discovery and DSM installation | Passed |
| Storage pool and volume creation | Passed |
| Initial drive check | Passed |
| Reserved network address | Passed |
| Windows SMB access | Passed |
| macOS SMB access | Passed |
| Cross-platform file visibility | Passed |
| Standard-user permissions | Passed |
| Remote access | Passed |
| Notification test | Passed |
| Configuration backup | Passed |
| Dedicated versioned data backup | Pending |

## Documentation

- [Complete Setup Guide](docs/setup-guide.md)
- [Security and Best Practices](docs/security-and-best-practices.md)
- [Validation and Troubleshooting](docs/validation-and-troubleshooting.md)
- [Backup and Recovery Roadmap](docs/backup-roadmap.md)

## Current Limitation

The current public example uses a single-drive storage pool.

```text
One drive failure = storage unavailable
```

A second compatible drive can later add one-drive fault tolerance. RAID improves availability, but it does not replace backup.

## Planned Next Phase

- Add a dedicated external backup drive
- Install Hyper Backup
- Configure versioned backups
- Enable backup rotation
- Schedule integrity checks
- Test file restoration
- Document the recovery workflow

## Security Notice

This repository intentionally excludes:

- Production IP addresses
- Real usernames
- QuickConnect identifiers
- Email addresses
- MAC addresses
- Serial numbers
- Screenshots containing sensitive infrastructure details
- Credentials, recovery codes, and encryption keys
