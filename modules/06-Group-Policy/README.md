# Group Policy

## Overview

Group Policy was implemented to centrally manage user and computer configurations across the Active Directory domain.

By applying Group Policy Objects (GPOs), administrative settings can be enforced automatically without requiring manual configuration on individual systems. This approach simplifies administration, improves consistency and strengthens the overall security posture of the environment.

---

# Why Group Policy

Group Policy is one of the most powerful features of Active Directory.

It allows administrators to centrally manage security settings, desktop configuration, software behavior and user restrictions while ensuring that every domain-joined computer follows the same policies.

For this laboratory, Group Policy was used to simulate common enterprise administration tasks.

---

# Group Policy Processing

Windows processes Group Policies using the standard Active Directory hierarchy.

1. Local Group Policy
2. Site
3. Domain
4. Organizational Unit (OU)

When multiple policies are applied, the most specific policy takes precedence unless inheritance or enforcement settings are configured differently.

---

# Implemented Group Policy Objects

The following Group Policy Objects were implemented throughout the laboratory.

| GPO | Purpose | Target |
|-----|---------|--------|
| Default Domain Policy | Password Policy & Account Lockout | Domain |
| Default Domain Controllers Policy | Default Domain Controller Configuration | Domain Controllers |
| GPO - Desktop Settings | Wallpaper and Lock Screen | Employees/IT |
| GPO - IT Users | User Configuration | Employees/IT |
| GPO - CMD Restriction | Restrict Command Prompt | Restricted Users |
| Domain Controllers | Domain Controller Security Hardening | Domain Controllers |

---

# Organizational Unit Linking

The implemented Group Policies were linked to specific Organizational Units to ensure that settings only affected their intended users or computers.

| GPO | Linked To |
|-----|-----------|
| GPO - Desktop Settings | Employees/IT |
| GPO - IT Users | Employees/IT |
| GPO - CMD Restriction | Restricted Users |
| Domain Controllers | Domain Controllers |

This approach demonstrates how Group Policy can be scoped to different departments while maintaining centralized administration.

---

# Desktop Settings

A dedicated Group Policy Object was created to standardize the desktop appearance across managed devices.

The policy configures both the desktop wallpaper and the lock screen using centrally stored resources hosted on the Domain Controller.

This ensures a consistent user experience throughout the environment.

---

## Wallpaper Policy

The desktop wallpaper is deployed automatically through Group Policy.

The wallpaper image is stored within a shared folder on the Domain Controller, allowing every targeted client to retrieve the same image during Group Policy processing.

Validation included:

- Successful wallpaper deployment
- Automatic application after user logon
- Centralized management

> *(Screenshot of deployed wallpaper will be added here.)*

---

## Lock Screen Policy

The lock screen image is deployed through the same Group Policy Object.

This guarantees that managed computers display a standardized lock screen without requiring manual configuration.

Validation included:

- Successful lock screen deployment
- Automatic application after policy refresh

> *(Screenshot of deployed lock screen will be added here.)*

---

# Shared Folder

A shared folder was created on the Domain Controller to centrally host enterprise resources.

This shared folder is currently used to store the wallpaper image deployed through Group Policy.

Validation included:

- Successful SMB share creation
- Successful client access
- Successful Group Policy access

> *(Screenshot of shared folder configuration will be added here.)*

---

# Command Prompt Restriction

A dedicated Group Policy was created to restrict access to the Windows Command Prompt for selected users.

The policy is linked only to the **Restricted Users** Organizational Unit, ensuring that other users remain unaffected.

Validation included:

- Command Prompt successfully blocked
- Restriction applied only to targeted users

> *(Screenshot of Command Prompt restriction will be added here.)*

---

# Password Policy

The laboratory uses the password policy configured through the **Default Domain Policy**.

The policy enforces centralized password requirements across the domain.

Configured settings include:

- Password complexity
- Password history
- Minimum password length
- Maximum password age

---

# Account Lockout Policy

Account lockout settings were configured to reduce the risk of password guessing attacks.

The policy automatically locks user accounts after repeated failed authentication attempts.

Configured settings include:

- Account lockout threshold
- Lockout duration
- Reset account lockout counter

---

# PowerShell Logging

PowerShell logging was enabled through Group Policy to improve visibility into PowerShell activity.

The following logging features were implemented:

- Module Logging
- Script Block Logging

These settings provide valuable information during security investigations and administrative troubleshooting.

Validation command:

```powershell
Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational" -MaxEvents 10
```

> *(Screenshot of PowerShell Operational Log will be added here.)*

---

# Windows Auditing

Advanced Audit Policy Configuration was implemented to improve monitoring of security-related events.

The laboratory currently audits:

- Process Creation
- Directory Service Changes
- Logon Events
- Security Group Management
- Credential Validation

Validation command:

```powershell
auditpol /get /category:*
```

> *(Screenshot of audit policy output will be added here.)*

---

# Security Baseline

The following security controls were implemented through Group Policy.

| Security Control | Status |
|------------------|--------|
| Desktop Wallpaper | ✅ Implemented |
| Lock Screen | ✅ Implemented |
| Command Prompt Restriction | ✅ Implemented |
| Password Policy | ✅ Implemented |
| Account Lockout Policy | ✅ Implemented |
| PowerShell Module Logging | ✅ Implemented |
| PowerShell Script Block Logging | ✅ Implemented |
| Windows Auditing | ✅ Implemented |

These policies demonstrate centralized administration while improving the security posture of the Active Directory environment.

---

# Validation

The Group Policy deployment was validated by confirming:

- Successful Group Policy processing
- Successful GPO application
- Successful wallpaper deployment
- Successful lock screen deployment
- Successful shared folder access
- Successful Command Prompt restriction
- Successful PowerShell logging
- Successful Windows auditing

Validation commands:

```powershell
gpupdate /force

gpresult /r

gpresult /h report.html

auditpol /get /category:*

Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational" -MaxEvents 10
```

---

# Lessons Learned

This module provided practical experience with:

- Active Directory Group Policy
- Organizational Unit design
- Centralized administration
- Enterprise policy deployment
- Desktop standardization
- Windows security configuration
- PowerShell logging
- Advanced Windows auditing
- Group Policy troubleshooting

---

# References

- Microsoft Learn
- Windows Group Policy Documentation
- Windows Security Documentation