# Linux Login Activity Analysis (wtmp, btmp)

This guide explains how to analyze **wtmp** and **btmp** login records on GNU/Linux system

---

### Overview

Linux systems maintain several binary accounting files that record user login activity.

The primary files used during post-mortem forensic investigations are:

| File | Purpose |
|---------|---------|
| `/var/log/wtmp` | Historical record of user logins, logouts, reboots, and shutdowns |
| `/var/log/btmp` | Historical record of failed login attempts |

# Basic Analysis Commands

## Review Historical Logins

```bash
last -f /var/log/wtmp
```

Example output:

```text
root     pts/0        192.168.1.50     Fri Jul 24 09:15 - 11:42  (02:27)
admin    pts/1        10.10.10.15      Fri Jul 24 07:05 - 07:33  (00:28)
reboot   system boot  5.15.0-91        Fri Jul 24 06:58
```

Output breakdown:

- Username
- Terminal
- Source IP address or hostname
- Session start and end time
- Session duration

## Review Failed Logins

```bash
last -f /var/log/btmp
```

Example output:

```text
root     ssh:notty    203.0.113.50     Fri Jul 24 03:21
admin    ssh:notty    203.0.113.50     Fri Jul 24 03:21
oracle   ssh:notty    203.0.113.50     Fri Jul 24 03:20
test     ssh:notty    203.0.113.50     Fri Jul 24 03:20
```

Output breakdown:

- Username targeted by the login attempt
- Authentication service
- Source IP address
- Time of the failed login attempt

## Review Reboots

```bash
last reboot -f /var/log/wtmp
```

Example output:

```text
reboot   system boot  5.15.0-91        Fri Jul 24 06:58
reboot   system boot  5.15.0-90        Thu Jul 23 18:12
reboot   system boot  5.15.0-90        Thu Jul 23 07:45
```

Output breakdown:

- Event type
- Boot event indicator
- Kernel version
- System boot time
