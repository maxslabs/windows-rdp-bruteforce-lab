# SOC Incident Report: RDP Brute Force Attempt

## Overview
This lab simulates a brute force attack against a Windows Server 2022 RDP service using a Kali Linux attacker VM. The objective is to observe and analyse authentication failures using Windows Event Logs.

---

## Detection Summary
Multiple failed authentication attempts were detected on the Windows Server.

- Event ID: 4625
- Logon Type: 3 (Network logon)
- Authentication Package: NTLM
- Logon Process: NtLmSsp

---

## Attack Source
- Attacker: Kali Linux VM
- Tooling: Nmap, xfreerdp
- Target: Windows Server 2022 RDP (3389)

---

## Observed Behaviour
- Repeated authentication failures against Administrator account
- Consistent source IP from attacker VM
- NTLM authentication attempts recorded in Security logs

---

## Conclusion
The system successfully logged and detected repeated failed authentication attempts consistent with brute force activity.
