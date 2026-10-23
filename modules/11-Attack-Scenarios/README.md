# Attack Scenarios — Kali Intrusion Testing

## Overview

A Kali Linux virtual machine is used to test the environment from the position of an
**internal attacker**. The workflow is iterative: run an attack, observe what is blocked or
detected, and harden accordingly. All testing is performed against this personal lab only.

---

# Methodology

1. Attack from Kali against the Domain Controller / network.
2. Observe the result (blocked, allowed, or detected in Wazuh).
3. Apply or confirm a control, then re-test.

---

# Tests Performed

| Test | Tool | Result |
|------|------|--------|
| Anonymous SMB/RPC enumeration (null session) | netexec, rpcclient | **Blocked** (access denied) |
| Kerberos user enumeration | kerbrute | Valid users found — **expected**, inherent to the protocol |
| AS-REP Roasting | impacket GetNPUsers | **No vulnerable accounts** (pre-auth enforced) |
| DNS zone transfer (AXFR) | dig | **Blocked** (transfer refused) |
| Password spraying | netexec | **Account lockout triggered** and detected in Wazuh |
| SMB relay exposure | — | **Mitigated** by SMB signing |
| Zerologon (CVE-2020-1472) | — | **Not exploitable** (patched; default on Server 2022) |

---

# What This Validated

- Anonymous enumeration and DNS zone transfer are closed.
- No accounts are AS-REP roastable (Kerberos pre-authentication is enforced).
- The account lockout policy (5 attempts / 15 minutes) works in practice and is detected.
- SMB signing mitigates relay attacks; the DC is patched against Zerologon.

---

# Key Takeaway

Testing confirmed the defences held, but also showed that **visibility** was the weak point:
the attacks happened with little being logged until auditing and Wazuh were in place. This is
what drove the monitoring work in the [Wazuh module](../10-Wazuh).

---

# Note on Scope

All techniques were run against a self-owned, isolated laboratory, for learning and
defensive validation only.

---

# Lessons Learned

- Validating controls by attacking them is more convincing than assuming they work.
- Some "findings" are protocol behaviour (Kerberos user enumeration), not misconfigurations.
- Detection coverage matters as much as the control itself.

---

# References

- MITRE ATT&CK
- Tool documentation: netexec, impacket, kerbrute
