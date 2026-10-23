# Wazuh — Centralised Logging & Monitoring

## Overview

Wazuh provides centralised logging, detection and automated response for the laboratory.
Agents on the Windows systems collect events and forward them to the Wazuh server, where
they are analysed against rules and stored for searching and alerting.

Under the hood, Wazuh runs on the **Wazuh indexer** (a fork of OpenSearch, which itself
derives from Elasticsearch) and the **Wazuh dashboard** (the equivalent of Kibana), so the
concepts map directly onto the Elastic Stack.

---

# Architecture

```
Windows Server (DC)  --agent--+
                              +-->  Wazuh Manager  -->  Indexer  -->  Dashboard
Windows 11 Client    --agent--+      (rules/decoders)   (storage)    (search/alerts)
                                             |
                                       Active Response
```

---

# Components

| Component | Role |
|-----------|------|
| Wazuh agent | Installed on the DC and the Windows 11 client; collects and ships events |
| Wazuh manager | Analyses events with rules and decoders |
| Wazuh indexer | Stores and indexes the data (OpenSearch fork) |
| Wazuh dashboard | Visualisation, search and alerting (Kibana equivalent) |

---

# Log Sources

- **Windows Security channel** — authentication, account and policy events
- **Sysmon** — detailed process creation, with command line and hashes

---

# Rules, Levels and Alerts

Each event is matched against a rule that assigns it a **severity level**. Events above a
threshold become **alerts**. Example observed during testing:

- Failed logon (Event ID **4625**) -> rule **60122** "Logon Failure", level 5
- Repeated failures -> brute-force detection

---

# Active Response

On a brute-force pattern, Wazuh triggers an **active response** that runs `netsh` to add a
Windows Firewall rule **blocking the source IP** automatically. This provides detection
*and* response, not just logging.

---

# MITRE ATT&CK

Alerts are mapped to MITRE ATT&CK techniques (for example, brute force = **T1110**), which
helps classify what an alert represents.

---

# Security Configuration Assessment (SCA)

Wazuh runs the **CIS Microsoft Windows Server 2022 Benchmark** against the Domain Controller
and reports a compliance score (current baseline: **28%**), used as a hardening roadmap.

---

# Validation

- Agents on the DC and the Windows 11 client show as **Active** in the dashboard.
- A deliberate failed logon appears in the Windows **Event Viewer** and in the **Wazuh
  dashboard** (rule 60122), proving the full pipeline: source -> agent -> indexer -> dashboard.
- The brute-force active response fired and blocked the source IP.

---

# Lessons Learned

- Enabling auditing only writes events to the Windows log; an agent is still needed to ship
  them to Wazuh.
- Sysmon greatly improves process-level visibility over the Security log alone.
- Detection without response is incomplete — active response closes the loop.

---

# References

- Wazuh Documentation
- MITRE ATT&CK
- CIS Benchmarks
