# Group Policy

## Overview

Group Policy centrally manages user and computer configuration across the Active
Directory domain. By applying Group Policy Objects (GPOs), security settings and
administrative configuration are enforced automatically on every domain-joined system,
without manual configuration.

The hardening in this environment is **split across several GPOs by function** (NTLM,
SMB, auditing, firewall) rather than being combined into a single object. This keeps each
policy focused and easy to target to the right scope.

---

# Group Policy Processing

Windows processes policies using the standard Active Directory hierarchy:

1. Local Group Policy
2. Site
3. Domain
4. Organizational Unit (OU)

When several policies apply, the most specific (closest to the object) wins unless
inheritance or enforcement is configured otherwise.

---

# Implemented Group Policy Objects

The following GPOs are deployed. Each is linked only where it should apply.

| GPO | Purpose | Linked to |
|-----|---------|-----------|
| Default Domain Policy | Password & account lockout policy | Domain |
| Default Domain Controllers Policy | Domain controller security (LDAP signing, SMB signing, secure channel) | Domain Controllers |
| GPO - NTLM Hardening | NTLMv2 enforcement, LDAP signing, channel binding, NTLM auditing, AutoPlay off, PowerShell logging | Domain |
| GPO - SMB Hardening | SMB signing (client and server) | Domain Controllers + Workstations |
| GPO - Audit Policy | Advanced audit configuration | Domain Controllers + Workstations |
| GPO - Windows Firewall | Windows Defender Firewall baseline | Workstations |
| GPO - Desktop Settings | Screen lock on inactivity | Company-Users |
| GPO - IT Users | Restrict access to Command Prompt | Company-Users/IT |
| MapContabilidade | Map a department network drive | Company-Users/Contabilidade |

---

# Password Policy (Default Domain Policy)

| Setting | Value |
|---------|-------|
| Minimum password length | 12 characters |
| Password complexity | Enabled |
| Enforce password history | 10 passwords |
| Maximum password age | 90 days |
| Store passwords using reversible encryption | Disabled |

---

# Account Lockout Policy (Default Domain Policy)

| Setting | Value |
|---------|-------|
| Account lockout threshold | 5 invalid attempts |
| Account lockout duration | 15 minutes |
| Reset account lockout counter after | 15 minutes |

These settings reduce the risk of password-guessing and brute-force attacks.

---

# Domain Controller Hardening (Default Domain Controllers Policy)

Configured directly on the Domain Controllers OU so it applies with the correct
precedence on the DCs:

- **LDAP server signing requirements: Require signing**
- SMB server signing (always / if client agrees)
- Secure channel data digitally encrypted or signed (always)

---

# NTLM Hardening

Applied at the domain level:

- **LAN Manager authentication level:** Send NTLMv2 response only, refuse LM & NTLM
- **LDAP client signing:** Require signing
- **LDAP channel binding:** Always
- **Restrict NTLM:** auditing enabled (incoming and in-domain)
- AutoPlay / AutoRun disabled on all drives
- PowerShell **Module Logging** and **Script Block Logging** enabled

---

# SMB Hardening

SMB signing is enforced on both the client and the server side, protecting file-sharing
traffic against tampering and relay (man-in-the-middle) attacks.

---

# Windows Auditing (Advanced Audit Policy)

Linked to Domain Controllers and Workstations, with *Force audit policy subcategory
settings* enabled. Audited subcategories include:

- Credential Validation
- Security Group Management
- Process Creation
- Directory Service Changes
- Logon / Logoff / Special Logon
- File System
- Audit Policy Change
- Sensitive Privilege Use

These events feed the centralised monitoring platform.

---

# Windows Firewall

Linked to Workstations:

- Firewall state: On
- Inbound connections: Block
- Outbound connections: Allow
- Protect all network connections: Enabled

---

# Desktop Settings (Screen Lock)

Linked to Company-Users. Enforces a password-protected screen saver after **600 seconds**
of inactivity, locking the session automatically.

---

# Command Prompt Restriction (GPO - IT Users)

Linked to the **Company-Users/IT** OU. Restricts access to the Windows Command Prompt for
users in that OU, demonstrating how a policy can be scoped to a single department.

> Note: the restriction does not block Windows PowerShell.

---

# Department Drive Mapping (MapContabilidade)

Linked to the **Company-Users/Contabilidade** OU. Uses Group Policy Preferences to map a
network drive automatically for Accounting users:

| Setting | Value |
|---------|-------|
| Drive letter | S: |
| Location | `\\DC01\Contabilidade` |
| Action | Update |
| Reconnect | Enabled |
| Label | Contabilidade |

This demonstrates automatic, per-department drive mapping — a very common enterprise
administration task.

---

# Validation

The Group Policy deployment was validated by confirming:

- Successful GPO processing and application
- Password and lockout policy enforced
- Screen lock applied after inactivity
- Command Prompt restriction applied only to the IT OU
- Department drive mapped automatically for Accounting users
- PowerShell logging and advanced auditing operational

Validation commands:

```powershell
gpupdate /force

gpresult /r

gpresult /h report.html

auditpol /get /category:*
```

---

# Lessons Learned

This module provided practical experience with:

- Active Directory Group Policy and OU-scoped linking
- Organising hardening by function across multiple GPOs
- Password, lockout and Kerberos policy
- NTLM, SMB and LDAP hardening
- Advanced Windows auditing
- Group Policy Preferences (drive mapping)
- Group Policy troubleshooting and reporting

---

# References

- Microsoft Learn
- Windows Group Policy Documentation
- Microsoft Security Baselines
