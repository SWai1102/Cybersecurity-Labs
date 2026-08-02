# Linux Security Hardening Lab

## Objective

This lab demonstrates practical Linux security administration, access-control review, patch verification, and system-hardening techniques using Ubuntu on WSL 2.

## Environment

- Windows 11
- WSL 2
- Ubuntu
- Visual Studio Code

## Activities

- Collected system and operating system information
- Reviewed package update status
- Reviewed current user identity and group membership
- Identified login-capable accounts
- Reviewed sudo privileges

## Security Relevance

Regular account, privilege, and patch reviews help reduce unauthorized access, privilege misuse, and exposure to known vulnerabilities.

## Progress

- [x] System information collection
- [x] Package update verification
- [x] User and group review
- [x] Login-capable account review
- [x] Sudo privilege review
- [x] File permission audit
- [x] Firewall configuration
- [ ] Authentication log analysis
- [ ] SSH hardening

## File Permission Audit

Three test files were configured with different access levels:

| File | Permission | Security purpose |
|---|---:|---|
| `public.txt` | `644` | Owner can modify; other users can only read |
| `private.txt` | `600` | Only the owner can read and modify |
| `script.sh` | `700` | Only the owner can read, modify, and execute |

Removing the execute permission from `script.sh` prevented the script from running, demonstrating how Linux permissions control program execution.

## Firewall Configuration

UFW was enabled with the following default policies:

- Incoming traffic: denied
- Outgoing traffic: allowed
- Routed traffic: disabled
- Logging level: low

A temporary TCP port 22 rule was created and removed to demonstrate firewall rule management. No inbound ports were left unnecessarily exposed.

## Listening Port Review

The `ss -tulpn` command was used to identify listening network services.

Observed services included:

- DNS resolution on port 53 through the WSL/systemd-resolved environment
- Local time synchronization through chronyd on UDP port 323

The services were primarily bound to loopback or WSL internal addresses. No unnecessary service was observed listening on all external interfaces.

## Security Finding

The system follows a default-deny inbound policy and currently has no unnecessary inbound firewall exceptions, reducing its exposed attack surface.

## Authentication Log Analysis

A temporary OpenSSH Server was configured to generate and review real authentication events.

### Test activities

- Started the SSH service
- Temporarily allowed TCP port 22 through UFW
- Performed one successful SSH login
- Performed one failed password authentication
- Reviewed successful login history using `last`
- Reviewed SSH authentication events using `journalctl`
- Removed the firewall exception
- Disabled and stopped the SSH service after testing

### Findings

The successful login record identified:

- User: `sam`
- Authentication method: password
- Source address: WSL host-side virtual network
- Session duration: approximately one minute

The failed authentication event recorded an incorrect password attempt for the same user and source address.

### Security relevance

SSH authentication logs can help identify unauthorized access attempts, password-guessing activity, suspicious source addresses, and unexpected successful sessions.

### Remediation

The temporary SSH firewall rule was removed and the SSH service was disabled after completing the test to avoid leaving an unnecessary network service exposed.