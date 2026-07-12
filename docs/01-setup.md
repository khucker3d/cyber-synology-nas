# Complete Setup Guide

## Overview

This guide documents the deployment of a two-bay Synology NAS as a secure personal cloud and cross-platform file server.

## 1. Install the Drive

1. Power off the NAS.
2. Insert a NAS-rated SATA drive.
3. Secure the drive tray.
4. Connect Ethernet.
5. Connect power.
6. Boot the NAS.
7. Wait for initialization.

## 2. Install DSM

1. Use the Synology discovery page or local network controller.
2. Connect to the detected NAS.
3. Install the latest version of DiskStation Manager.
4. Confirm that the installed drive may be erased.
5. Create a named administrator account.
6. Use a unique password.
7. Avoid using the built-in `admin` account.

Example:

```
Hostname: nas-storage-01
Administrator: nasadmin
```

## 3. Create the Storage Pool

1. Open **Storage Manager**.
2. Create a new storage pool.
3. Select **Synology Hybrid RAID**.
4. Select the installed drive.
5. Enable the initial drive check.
6. Use the available capacity.
7. Complete the wizard.

Example:

```
Storage Pool: Storage Pool 1
RAID Type: SHR
Drive Count: 1
```

A one-drive SHR pool has no fault tolerance.

## 4. Create the Volume

1. Create a volume on the new pool.
2. Use the filesystem recommended by DSM.
3. Allocate the available capacity.
4. Allow the drive check to complete.

Validate:

```
Storage Pool: Healthy
Volume: Healthy
Drive: Healthy
```

## 5. Reserve the Network Address

Create a DHCP reservation in the managed network controller.

```
Hostname: nas-storage-01
Reserved IP: 192.168.50.30
```

Keep DSM configured for DHCP so the network controller remains the source of truth.

Local access:

```
https://192.168.50.30:5001
```

## 6. Update DSM and Packages

1. Open **Control Panel → Update & Restore**.
2. Install DSM updates.
3. Restart if required.
4. Open **Package Center → Installed**.
5. Update installed Synology packages.
6. Avoid unnecessary applications and beta packages.

## 7. Configure Time

1. Open **Control Panel → Regional Options → Time**.
2. Select the correct time zone.
3. Enable NTP synchronization.
4. Confirm the displayed date and time.

## 8. Harden Administrator Access

1. Create or verify the named administrator account.
2. Enable multi-factor authentication.
3. Store recovery information outside the NAS.
4. Disable the built-in `admin` account.
5. Disable the `guest` account.

## 9. Create a Standard User

Create a daily-use account:

```
Username: nasuser
Group: users
Administrator membership: No
```

Use it for SMB, mobile access, and routine file operations.

## 10. Enable Login Protection

Recommended baseline:

```
Auto Block:
5 failed attempts within 10 minutes
Temporary block: 1 day
```

```
Account Protection:
5 failed attempts within 10 minutes
Protection duration: 30 minutes
```

## 11. Create the Shared Folder

Create:

```
Shared Folder: Personal
Location: Volume 1
```

Recommended settings:

- Recycle Bin enabled
- Guest access disabled
- Unauthorized files hidden
- Encryption evaluated separately

Permissions:

| Account | Access |
|---|---|
| `nasuser` | Read/Write |
| `nasadmin` | Read/Write |
| `guest` | No access |
| Other users | No access unless explicitly assigned |

## 12. Configure SMB

Enable SMB under **Control Panel → File Services → SMB**.

Use:

```
Maximum SMB protocol: SMB3
Minimum SMB protocol: SMB2
SMB1: Disabled
WINS: Disabled
Transport encryption: Client defined
```

Enable opportunistic locking and supported SMB leasing features.

## 13. Validate Windows Access

Open File Explorer and enter:

```
\\192.168.50.30
```

Authenticate with the standard NAS account.

Test file creation, editing, deletion, and recycle-bin behavior.

## 14. Validate macOS Access

In Finder:

```
Go → Connect to Server
```

Enter:

```
smb://192.168.50.30
```

Authenticate with the same standard NAS account and confirm cross-platform file visibility.

## 15. Configure Remote Access

Enable Synology QuickConnect and validate access from a device outside the home network.

Do not directly expose:

```
TCP 445
TCP 5001
```

Do not forward SMB to the internet.

## 16. Schedule S.M.A.R.T. Tests

Quick test:

```
Frequency: Monthly
Time: 02:00
Target: All supported drives
```

Extended test:

```
Frequency: Every six months
Time: 03:00
Target: All supported drives
```

## 17. Schedule Data Scrubbing

Recommended baseline:

```
Target: Storage Pool 1
Frequency: Every three months
Maintenance window: Overnight
```

## 18. Configure Notifications

Enable email alerts for:

- S.M.A.R.T. failures
- Bad sectors and I/O errors
- Storage-pool degradation
- Volume failures
- Low capacity
- High temperatures
- Abnormal shutdowns
- Backup failures
- Failed sign-ins
- Account-protection events
- Update problems

Send and verify a test notification.

## 19. Back Up DSM Configuration

Export a configuration backup:

```
nas-storage-01-config-YYYY-MM-DD.dss
```

Store it outside the NAS.

Enable encrypted automatic DSM configuration backup where appropriate.

Configuration backup does not include shared-folder data.

## 20. Plan Data Backup

Do not back up to another folder on the same internal drive.

Use a separate destination:

- Dedicated external USB drive
- Another NAS
- Supported cloud destination
- Remote backup server

Test file restoration after the first successful backup.
