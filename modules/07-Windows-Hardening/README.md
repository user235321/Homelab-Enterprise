# Windows Hardening

## Overview

Windows hardening was implemented to improve the security posture of the laboratory by reducing the attack surface and enabling security monitoring.

The implemented controls follow common enterprise security practices and demonstrate how Windows environments can be secured through centralized configuration and security policies.

The objective was not only to secure the environment but also to gain practical experience with enterprise hardening techniques commonly encountered in production infrastructures.

---

# Security Objectives

The security baseline was designed to achieve the following objectives:

- Reduce the attack surface
- Protect authentication mechanisms
- Secure network communication
- Improve system monitoring
- Enable security auditing
- Strengthen PowerShell visibility

---

# Implemented Security Controls

The following security controls were implemented.

| Security Control | Status |
|------------------|--------|
| Windows Defender | Enabled |
| Windows Firewall | Enabled |
| SMB Signing | Enabled |
| SMBv1 Disabled | Implemented |
| NTLM Hardening | Implemented |
| LDAP Signing | Implemented |
| AutoRun Disabled | Implemented |
| PowerShell Module Logging | Enabled |
| PowerShell Script Block Logging | Enabled |
| Process Auditing | Enabled |
| Directory Service Auditing | Enabled |

---

# Windows Defender

Microsoft Defender Antivirus remains enabled throughout the laboratory.

Real-time protection is active and provides baseline malware protection for Windows systems.

Validation included:

```powershell
Get-MpComputerStatus
```

> *(Screenshot of Defender status will be added here.)*

---

# Windows Firewall

Windows Defender Firewall remains enabled using the default enterprise configuration.

Inbound connections are blocked unless explicitly permitted.

Validation included:

```powershell
Get-NetFirewallProfile
```

> *(Screenshot of Firewall configuration will be added here.)*

---

# SMB Hardening

SMB was hardened to reduce exposure to legacy protocols and improve the security of file sharing.

---

## SMB Signing

SMB Signing was enabled to ensure message integrity during SMB communications.

Validation included:

```powershell
Get-SmbServerConfiguration | Select EnableSecuritySignature,RequireSecuritySignature

Get-SmbClientConfiguration | Select EnableSecuritySignature,RequireSecuritySignature
```

> *(Screenshot of SMB Signing validation will be added here.)*

---

## SMBv1 Removal

The SMBv1 protocol remains disabled within the environment.

Disabling SMBv1 reduces exposure to legacy attacks targeting obsolete SMB implementations.

Validation included:

```powershell
Get-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
```

> *(Screenshot of SMBv1 validation will be added here.)*

---

# NTLM Hardening

NTLM authentication was hardened by enforcing NTLMv2 authentication and disabling LM hash storage.

Validation included:

```powershell
Get-ItemProperty "HKLM:\SYSTEM\CurrentControlSet\Control\Lsa" |
Select LmCompatibilityLevel,NoLMHash
```

> *(Screenshot of NTLM validation will be added here.)*

---

# LDAP Signing

LDAP Signing was enabled to protect communications between clients and the Domain Controller against man-in-the-middle attacks.

Validation included:

```powershell
Get-ItemProperty "HKLM:\SYSTEM\CurrentControlSet\Services\NTDS\Parameters" |
Select LDAPServerIntegrity
```

> *(Screenshot of LDAP Signing validation will be added here.)*

---

# AutoRun Protection

AutoRun and AutoPlay were disabled to prevent automatic execution of software from removable media.

This configuration reduces the risk of malware propagation through USB devices.

> *(Screenshot of AutoRun policy will be added here.)*

---

# PowerShell Security

PowerShell logging was enabled to improve visibility into administrative activity.

---

## Module Logging

Module Logging records executed PowerShell module activity.

---

## Script Block Logging

Script Block Logging records executed PowerShell code, improving forensic capabilities during investigations.

Validation included:

```powershell
Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational" -MaxEvents 10
```

> *(Screenshot of PowerShell logs will be added here.)*

---

# Windows Auditing

Advanced auditing was configured to improve monitoring of security events.

---

## Process Auditing

Process Creation auditing was enabled to record process execution.

---

## Directory Service Auditing

Directory Service Changes auditing records modifications made to Active Directory.

---

## Security Event Logging

Security events are available through Windows Event Viewer.

Validation included:

```powershell
auditpol /get /category:*
```

> *(Screenshot of audit policy output will be added here.)*

---

# Security Validation

The hardening configuration was validated by confirming:

- Defender enabled
- Firewall enabled
- SMB Signing enabled
- SMBv1 disabled
- NTLM hardened
- LDAP Signing enabled
- AutoRun disabled
- PowerShell logging operational
- Advanced auditing operational

---

# Lessons Learned

This module provided practical experience with:

- Windows Security Hardening
- SMB Security
- LDAP Security
- NTLM Hardening
- Windows Firewall
- Microsoft Defender
- PowerShell Logging
- Windows Auditing
- Security Validation

---

# References

- Microsoft Learn
- Microsoft Security Baselines
- Windows Security Documentation