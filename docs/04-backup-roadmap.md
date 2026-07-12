# Backup and Recovery Roadmap

## Current State

```
NAS internal drive:
Primary centralized storage

Transfer drive:
Temporary file movement

Dedicated backup drive:
Pending
```

The transfer drive remains separate from the NAS backup workflow.

## Recommended Design

```
Synology NAS
     |
Hyper Backup
     |
Dedicated external USB drive
```

A second offsite or offline copy should protect the most important files.

## Planned Tasks

1. Obtain a dedicated external backup drive.
2. Connect it directly to the NAS.
3. Confirm detection under External Devices.
4. Install Hyper Backup.
5. Create a multi-version backup task.
6. Select protected shared folders.
7. Schedule overnight backups.
8. Enable version rotation.
9. Schedule integrity checks.
10. Run the first backup.
11. Test file restoration.
12. Document recovery steps.
13. Periodically disconnect or rotate the backup drive when appropriate.

## Capacity Guidance

| Backup drive size | Use case |
|---|---|
| 4 TB | Basic backup capacity |
| 6 TB | More version history |
| 8 TB | Longer retention and future growth |

## Recovery Objectives

Document:

- Which folders are critical
- Acceptable data-loss window
- Acceptable restoration time
- Location of configuration exports
- Location of encryption passwords
- Location of recovery codes
- Restore test dates and results

## 3-2-1 Direction

Work toward:

- Three copies of important data
- Two different storage media
- One copy offline or offsite
