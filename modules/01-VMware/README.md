# VMware Workstation

## Overview

VMware Workstation Pro was selected as the hypervisor for this laboratory due to its stability, flexibility and support for complex virtual networking. All virtual machines used throughout the project are hosted on VMware, providing an isolated environment for testing enterprise infrastructure.

---

# Why VMware

VMware Workstation Pro was chosen because it provides:

- Multiple virtual network types
- Snapshot support
- Hardware customization
- Reliable virtual networking
- Easy virtual machine management

---

# Host Specifications

| Component | Specification |
|-----------|---------------|
| Operating System | Windows 11 |
| Hypervisor | VMware Workstation Pro |
| Memory | 16 GB RAM |
| Processor | Intel Core i7-13620H |
| Storage | SSD |

---

# Virtual Machine Specifications

| Virtual Machine | vCPU | RAM | Disk |
|-----------------|------|-----|------|
| pfSense | 2 | 4 GB | 20 GB |
| Windows Server | 2 | 4 GB | 60 GB |
| Windows 11 Enterprise | 2 | 4 GB | 60 GB |
| Ubuntu Server | 2 | 4 GB | 20 GB (system) + 4 × 10 GB (data: RAID 5 + spare) |

---

# Virtual Network Configuration

Two virtual networks were configured.

| Network | Type | Purpose |
|----------|------|---------|
| VMnet8 | NAT | Internet access |
| VMnet1 | Host-Only | Internal enterprise network |

---

# VMware Network Editor

The VMware Virtual Network Editor was used to configure the networking environment.

Configuration summary:

| Network | Configuration |
|----------|---------------|
| VMnet8 | NAT |
| VMnet1 | Host-Only |

---

# Snapshots

Snapshots were used before major configuration changes to allow quick recovery in case of configuration errors.

Examples include:

- Before Active Directory installation
- Before Group Policy deployment
- Before Windows Hardening

---

# Resource Allocation

Resource allocation was planned to balance performance while remaining compatible with a host machine equipped with 16 GB of RAM.

The virtual machines were configured with only the resources required for their intended roles, allowing all systems to run simultaneously without excessive resource consumption.

---

# Validation

The virtualization environment was validated by confirming:

- All virtual machines boot successfully
- Internal network communication
- Internet connectivity through pfSense
- Stable resource usage

---

# Lessons Learned

This module provided practical experience with:

- VMware Workstation Pro
- Virtual networking
- Resource planning
- Enterprise lab design
- Snapshot management

---

# References

- VMware Workstation Documentation