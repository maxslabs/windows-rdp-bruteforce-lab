# Windows RDP Brute Force Detection Lab

## Overview

This project simulates a real-world brute force attack against a Windows Remote Desktop Protocol (RDP) service and demonstrates detection, logging, and analysis from a SOC (Security Operations Center) perspective.

The goal is to replicate attacker behavior, observe Windows security telemetry, and map observed activity to MITRE ATT&CK techniques.

## Attack Flow Diagram

The diagram below illustrates the end-to-end attack chain from reconnaissance through brute-force authentication attempts and Windows Security log detection.

![RDP Brute Force Attack Flow](./diagrams/attack-flow.png)

---

## Objectives

- Simulate RDP brute-force login attempts from a Kali Linux attacker machine
- Capture and analyze Windows Security Event Logs
- Identify failed authentication patterns (Event ID 4625)
- Understand how Windows logs detect authentication abuse
- Map observed behavior to MITRE ATT&CK framework
- Build a structured SOC-style incident report
- Document full attack lifecycle with evidence and diagrams

---

## Lab Environment

### Virtual Machines

- **Attacker Machine:** Kali Linux
- **Target Machine:** Windows Server (RDP enabled)
- **Network:** NAT / Host-only isolated lab network

### Services Under Test

- Remote Desktop Protocol (TCP 3389)
- Windows Security Event Logging
- Local Windows authentication subsystem

---

## Attack Scenario

The attacker attempts to gain unauthorized access to the Windows machine using repeated password guesses against an exposed RDP service.

This simulates:
- Credential stuffing
- Password spraying
- Brute-force authentication attacks

---

## Attack Flow Diagram

The following diagram illustrates the full attack lifecycle from reconnaissance to failed authentication attempts and logging:

![RDP Brute Force Attack Flow](./diagrams/attack-flow.png)

> Diagram generated using Graphviz on Linux as part of the lab documentation process.

---

## Detection & Logging

Windows Security logs captured multiple authentication failures during the attack simulation.

### Primary Detection Source

- **Event ID 4625** — An account failed to log on

### Key Fields Observed

- Logon Type: 10 (RemoteInteractive / RDP)
- Source IP: Kali Linux attacker machine
- Username attempts: multiple invalid usernames/passwords
- Failure Reason: Unknown username or bad password

### Example Observations

- Rapid repeated login failures within short time intervals
- Multiple authentication attempts against the same account
- Consistent source IP across all failed attempts

---

## MITRE ATT&CK Mapping

| Technique ID | Technique Name | Description |
|-------------|----------------|-------------|
| T1110 | Brute Force | Repeated login attempts to guess credentials |
| T1078 | Valid Accounts (attempted) | Attempt to access system using valid or guessed credentials |
| T1021.001 | Remote Services: RDP | Use of RDP as the attack vector |

---

## Evidence Collected

All evidence is stored in the `/evidence` directory:

- Nmap scan results (`/evidence/scans`)
- RDP brute-force attempt screenshots (`/evidence/attacks`)
- Windows Event Logs showing failed logins (`/evidence/windows-logs`)
- Supporting screenshots (`/evidence/screenshots`)

---

## Key Findings

- Windows logs reliably captured all failed authentication attempts via Event ID 4625
- RDP brute-force activity is highly detectable through log pattern analysis
- Attackers generate identifiable behavior patterns (frequency + repetition)
- Log correlation is critical for identifying automated attack tools
- Proper monitoring would allow early detection before compromise

---

## Security Recommendations

- Enforce account lockout policies after repeated failed logins
- Restrict RDP access using firewall rules or VPN-only access
- Enable Network Level Authentication (NLA)
- Use multi-factor authentication (MFA) for remote access
- Monitor and alert on Event ID 4625 spikes
- Limit RDP exposure to trusted IP ranges only

---

## Tools Used

- Kali Linux (attack simulation)
- Windows Server (target system)
- Event Viewer (log analysis)
- Nmap (reconnaissance)
- Graphviz (attack flow diagram generation)

---
