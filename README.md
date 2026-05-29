# Windows RDP Brute Force SOC Lab

Kali Linux is used to simulate brute force RDP attacks against a Windows Server 2022 VM.

Windows logs (Event ID 4625) are used to detect failed authentication attempts and analyse attacker behaviour.

# windows-rdp-bruteforce-lab
# Windows RDP Brute Force SOC Lab  Kali Linux is used to simulate brute force RDP attacks against a Windows Server 2022 VM.  Windows logs (Event ID 4625) are used to detect failed authentication attempts and analyse attacker behaviour.

## Detection Logic (SOC Rule Example)

A SIEM alert could be triggered under the following conditions:

- Event ID: 4625
- Logon Type: 3
- Same source IP within 5–10 minutes
- Repeated failures against the same account (e.g. Administrator)

Threshold example:
- ≥5 failed logins within 5 minutes → High severity alert
