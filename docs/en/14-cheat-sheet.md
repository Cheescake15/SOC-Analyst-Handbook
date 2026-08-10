# 14 — Cheat Sheet

[← Back to the English contents](README.md) | [Magyar változat](../hu/14-cheat-sheet.md)

## Introduction

This chapter is a quick reference for the most important concepts introduced earlier

It does not replace the full chapters

Use it to quickly find:

- terminology
- Windows Event IDs
- Windows and Linux commands
- investigation questions
- ATT&CK concepts
- incident response steps

## 1. SOC Basics

| Term | Short meaning |
|---|---|
| SOC | Security Operations Center |
| Alert | a notification that may require investigation |
| Event | something recorded by a system |
| Incident | a confirmed or likely security problem |
| Triage | quick first assessment |
| Escalation | passing a case to a higher support level |
| Playbook | predefined response or investigation steps |
| Runbook | detailed operational instructions |
| False positive | incorrect alert |
| False negative | malicious activity that was missed |

## 2. Network Basics

| Term | Short meaning |
|---|---|
| IP address | network address of a device |
| MAC address | hardware-level network identifier |
| DNS | maps domain names to IP addresses |
| DHCP | automatically provides network settings |
| TCP | connection-oriented protocol |
| UDP | connectionless protocol |
| ICMP | network status and error messages |
| NAT | translates internal and external addresses |
| Port | logical service endpoint |
| HTTPS | encrypted HTTP communication |

## 3. Common Ports

| Port | Service |
|---:|---|
| 20/21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 110 | POP3 |
| 143 | IMAP |
| 443 | HTTPS |
| 445 | SMB |
| 3389 | RDP |

A port number alone does not prove malicious activity.

## 4. Useful Windows Event IDs

| Event ID | Meaning |
|---:|---|
| 4624 | successful logon |
| 4625 | failed logon |
| 4688 | new process created |
| 4720 | user account created |
| 4728 | member added to a global security group |
| 4732 | member added to a local security group |
| 4740 | user account locked out |
| 7045 | service installed |

Always review the event details as well.

## 5. Windows Quick Commands

```powershell
Get-Process
Get-Service
Get-ScheduledTask
Get-WinEvent -LogName System -MaxEvents 20
eventvwr.msc
```

## 6. Linux Quick Commands

```bash
whoami
who
id
groups
ls -l
ps aux
ss -tulpen
journalctl -n 20
systemctl --type=service --state=running
crontab -l
```

## 7. Linux Permissions

| Symbol | Meaning |
|---|---|
| r | read |
| w | write |
| x | execute |

Example:

```text
-rwxr-x---
```

Owner can read, write, and execute

Group can read and execute

Others have no access

## 8. Important Linux Directories

| Directory | Meaning |
|---|---|
| /home | user files |
| /etc | configuration |
| /var/log | logs |
| /tmp | temporary files |
| /usr/bin | programs |
| /root | root home directory |
| /proc | process and kernel information |

## 9. Useful Log Fields

Look for:

- timestamp
- user
- hostname
- source IP
- destination IP
- ports
- process
- command line
- file name
- hash
- event ID
- result

## 10. Quick Investigation Questions

```text
1. What happened?
2. When did it happen?
3. Who or what is involved?
4. What happened before?
5. What happened after?
6. Could it be normal?
7. What makes it suspicious?
8. Which data is missing?
9. Is there related CTI?
10. What should happen next?
```

## 11. SIEM Basics

| Term | Short meaning |
|---|---|
| SIEM | central security log collection and analysis |
| Ingestion | receiving data |
| Parsing | extracting fields |
| Normalisation | standardising fields |
| Query | searching data |
| Detection Rule | alert logic |
| Correlation | connecting related events |
| Dashboard | overview screen |
| Severity | alert importance |
| Tuning | improving a rule |

## 12. Detection Engineering Summary

```text
Understand the threat
↓
Choose the data source
↓
Write detection logic
↓
Test
↓
Review false positives
↓
Tune
↓
Document
↓
Review later
```

## 13. False Positive and False Negative

### False positive

The system alerts, but no real threat exists.

### False negative

A real threat occurs, but the detection misses it.

## 14. Sigma Quick Reference

Common fields:

```text
title
logsource
detection
condition
falsepositives
level
tags
```

Example:

```yaml
title: Failed Windows Logon

logsource:
  product: windows
  service: security

detection:
  selection:
    EventID: 4625
  condition: selection

level: low
```

## 15. CTI Basics

| Term | Short meaning |
|---|---|
| CTI | analysed threat information |
| Threat actor | attacker or attacker group |
| IoC | technical indicator of compromise |
| TTP | attacker tactics, techniques, and procedures |
| Feed | continuously updated threat source |
| Confidence | analyst confidence level |
| TLP | information-sharing rule |
| STIX | structured CTI format |
| TAXII | CTI transport mechanism |

## 16. Common IoCs

- IP address
- domain
- URL
- file hash
- email address
- file name

An IoC alone does not always prove an attack.

## 17. TLP 2.0

| Label | Short meaning |
|---|---|
| TLP:RED | very restricted sharing |
| TLP:AMBER | limited sharing |
| TLP:GREEN | sharing within a community |
| TLP:CLEAR | unrestricted sharing |

## 18. MITRE ATT&CK Basics

| Term | Meaning |
|---|---|
| Tactic | attacker goal |
| Technique | how the goal is achieved |
| Sub-technique | more specific technique |
| Procedure | real implementation |
| Group | known threat actor |
| Software | malware or attacker tool |
| Matrix | visual organisation of tactics and techniques |

## 19. Common ATT&CK Tactics

- Reconnaissance
- Initial Access
- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Credential Access
- Discovery
- Lateral Movement
- Collection
- Command and Control
- Exfiltration
- Impact

Understanding the logic is more important than memorising the full list.

## 20. ATT&CK Example

```text
T1059.001 — PowerShell
```

This is the PowerShell sub-technique of Command and Scripting Interpreter.

## 21. Malware Types

| Type | Short meaning |
|---|---|
| Virus | may spread by attaching to files |
| Worm | can spread automatically |
| Trojan | pretends to be harmless software |
| Ransomware | encrypts or blocks access and demands payment |
| Spyware | monitors and collects information |
| Keylogger | records keystrokes |
| Backdoor | provides hidden access |
| Downloader | downloads additional malware |
| Dropper | installs another malware component |
| Bot | remotely controlled infected device |
| Rootkit | may hide attacker presence |

## 22. Malware Investigation

Check:

- file name
- file path
- hash
- process
- parent process
- network connections
- antivirus alerts
- appearance on other devices

Do not run unknown malware on your own computer.

## 23. Incident Response Summary

```text
Preparation
↓
Detection and Analysis
↓
Containment
↓
Eradication
↓
Recovery
↓
Lessons Learned
```

## 24. Incident Response Terms

| Term | Meaning |
|---|---|
| Triage | initial assessment |
| Containment | limiting spread |
| Eradication | removing attacker presence |
| Recovery | safe restoration |
| Evidence | information preserved for investigation |
| Chain of Custody | documentation of evidence handling |
| Escalation | passing the case onward |
| Lessons Learned | post-incident improvement |

## 25. Phishing Checklist

Check:

- sender
- domain
- link destination
- attachment
- urgency
- credential request
- other recipients
- clicks
- credential submission
- related CTI

## 26. Suspicious PowerShell Checklist

Check:

- user
- computer
- command line
- parent process
- EncodedCommand
- external connection
- created file
- scheduled task
- antivirus alert
- related events

## 27. Failed Logon Checklist

Check:

- count
- time window
- user
- IP address
- other targeted accounts
- successful logon afterwards
- whether the source is known
- similar previous activity

## 28. SSH Checklist

Check:

- source IP
- user
- failed attempts
- successful logon
- sudo
- cron
- new files
- new SSH keys
- external connections

## 29. Ransomware Checklist

Check:

- number of affected devices
- mass file modification
- ransom note
- common process
- common user
- file-server impact
- backup status
- EDR alerts
- signs of spread

Ransomware suspicion may require rapid escalation.

## 30. Prioritisation Questions

An alert may be more urgent when:

- it affects a privileged account
- it affects a critical server
- several systems are involved
- it suggests data theft
- active malware is involved
- communication with attacker infrastructure exists
- the activity spreads quickly
- business operations are at risk

## 31. Incident Note Template

```text
Alert:
[alert name]

Time:
[time]

User:
[user]

Host:
[device]

Source IP:
[IP]

What happened:
[short description]

Timeline:
[events]

Checks performed:
[checks]

Known facts:
[confirmed facts]

Unknown:
[missing information]

Assessment:
[assessment]

Next step:
[next action]
```

## 32. Useful Analyst Language

```text
Observed
Confirmed
Likely
Possible
No evidence found
Further investigation required
User confirmation pending
Activity appears legitimate
Escalation recommended
```

These phrases help separate facts from assumptions.

## 33. Beginner Reminders

- Do not assume more than the evidence supports.
- Always build a timeline.
- Check user, host, and IP context.
- Search for related events.
- One IoC does not always prove an attack.
- One Event ID does not always prove an attack.
- PowerShell itself is not malicious.
- Port 443 itself is not suspicious.
- False positives are part of SOC work.
- Document missing information.
- Escalate high-risk uncertainty.
- Do not investigate systems without authorisation.
- Do not run unknown malware on a normal workstation.

## 34. Final Thinking Pattern

```text
What happened?
↓
Why might it matter?
↓
What evidence do I have?
↓
What normal explanation is possible?
↓
What information is missing?
↓
What happened before and after?
↓
How serious is the risk?
↓
What should happen next?
```

This reasoning process is one of the most important lessons of the handbook.

## References

This quick reference is based on the official and professional sources used throughout the previous chapters, including:

1. NIST  
   **Cybersecurity Framework 2.0**  
   https://www.nist.gov/cyberframework

2. NIST  
   **SP 800-61 Rev. 3**  
   https://csrc.nist.gov/pubs/sp/800/61/r3/final

3. MITRE ATT&CK  
   https://attack.mitre.org/

4. Microsoft Learn  
   **Microsoft Sentinel documentation**  
   https://learn.microsoft.com/en-us/azure/sentinel/

5. Sigma Detection Format  
   https://sigmahq.io/docs/

6. FIRST  
   **Traffic Light Protocol 2.0**  
   https://www.first.org/tlp/

7. Hungarian National Cyber Security Center  
   https://nki.gov.hu/

---

[← Previous chapter](13-practical-examples.md) | [Back to contents](README.md) | [Next chapter →](15-references.md)
