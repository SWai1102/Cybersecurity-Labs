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

UFW was configured using a default-deny inbound policy and a default-allow outbound policy.

### Applied policy

- Incoming connections: denied by default
- Outgoing connections: allowed by default
- Only explicitly required ports should be permitted
- A temporary SSH rule was created and removed to demonstrate firewall rule management

### Security relevance

A default-deny inbound policy reduces the attack surface by preventing unsolicited access to services unless they have been explicitly approved.