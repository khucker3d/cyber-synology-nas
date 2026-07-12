# Validation and Troubleshooting

## Validation Checklist

| Test | Result |
|---|---|
| NAS discovered | Passed |
| DSM installed | Passed |
| Storage pool created | Passed |
| Volume created | Passed |
| Initial drive check completed | Passed |
| Storage healthy | Passed |
| Reserved address configured | Passed |
| Administrator MFA enabled | Passed |
| Built-in accounts disabled | Passed |
| Standard user created | Passed |
| SMB enabled | Passed |
| Windows access | Passed |
| macOS access | Passed |
| Cross-platform visibility | Passed |
| Remote access | Passed |
| S.M.A.R.T. schedules | Passed |
| Data scrubbing schedule | Passed |
| Email notifications | Passed |
| Configuration export | Passed |
| Dedicated data backup | Pending |

## Drive Check Appears Stuck

Symptoms:

- Progress remains at the same percentage
- DSM browser page becomes unresponsive

Actions:

1. Confirm DSM is still reachable.
2. Check drive health in Storage Manager.
3. Review disk activity in Resource Monitor.
4. Allow time for the task to continue.
5. Do not interrupt power or remove the drive.
6. Reopen DSM if only the browser session crashed.

Storage tasks continue on the NAS independently of the browser page.

## DHCP Reservation Fails

Check:

- The address is unused
- The address belongs to the correct subnet
- The correct LAN is selected
- The NAS MAC address is correct
- The network controller is the DHCP server
- No existing reservation uses the same IP or MAC

## User Shows Password Pending

Possible cause:

- DSM email notifications are not yet configured

Resolution:

1. Edit the user.
2. Assign the password manually.
3. Confirm the account belongs only to the standard users group.
4. Verify the status changes to normal.

## Local Address Fails Away From Home

A private address such as:

```
192.168.50.30
```

is available only on the local network or through a VPN.

Use the approved remote-access method when offsite.

## SMB Authentication Problems

Check:

- SMB service is enabled
- SMB2 or SMB3 is supported by the client
- The standard NAS account has share permissions
- Guest access is not being used
- Cached Windows credentials are not conflicting
- The username is the NAS account, not necessarily the local computer username

## Restore Validation

A backup is not considered complete until a file can be restored successfully.

Test:

1. Back up a small sample folder.
2. Delete or rename a test file.
3. Restore it to an alternate location.
4. Compare the restored content.
5. Record the result.
