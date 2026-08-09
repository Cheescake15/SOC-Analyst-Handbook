# 13 — Practical Examples

[← Back to the English contents](README.md) | [Magyar változat](../hu/13-practical-examples.md)

## Introduction

Previous chapters introduced SOC operations, networks, Windows and Linux, log analysis, SIEM, CTI, MITRE ATT&CK, incident response, malware, and detection engineering.

This chapter connects those topics through simple practical examples.

The goal is not to perform real attacks.

The goal is to practise analyst thinking:

```text
What do I see?
What could it mean?
What information is missing?
What should I check next?
When should I escalate?
```

## 1. A Simple Investigation Method

A beginner can use the same basic questions for many alerts.

1. What happened?
2. When did it happen?
3. Which user, device, IP, file, or process is involved?
4. What happened before and after it?
5. Could there be a normal explanation?
6. What makes it suspicious?
7. Which information is missing?
8. What should happen next?

## 2. Example 1 — Multiple Failed Logons

```text
User: anna
Failed logons: 18
Time window: 5 minutes
Source IP: 10.10.5.24
```

Possible explanations include an incorrect password, a misconfigured application, or brute-force activity.

Useful checks include:

1. Was there a successful logon afterwards?
2. Is the source IP known?
3. Were other accounts targeted?
4. Does the user recognise the activity?
5. Has this happened before?

A successful logon after repeated failures makes the sequence more interesting.

## 3. Example 2 — Phishing Email

```text
Subject: Urgent password expiration
Sender: support@example-security-mail.com
Link: login-example-secure.com
```

Check:

- whether the sender domain is legitimate
- where the link leads
- whether other users received it
- whether anyone clicked
- whether credentials were entered
- whether CTI sources know the domain

Phishing can map to the Initial Access tactic in MITRE ATT&CK.

## 4. Example 3 — Suspicious PowerShell

```text
Process: powershell.exe
Parent process: winword.exe
User: bela
```

PowerShell itself is legitimate.

Word starting PowerShell may deserve more investigation.

Check:

1. which document was opened
2. where it came from
3. the PowerShell command line
4. whether encoded commands were used
5. whether an external connection occurred
6. whether new files appeared
7. whether antivirus alerted

Possible ATT&CK mapping:

```text
T1059.001 — PowerShell
```

## 5. Example 4 — Malware Alert

```text
Threat detected: Trojan
File: C:\Users\user\AppData\Local\Temp\update.exe
```

Check:

- whether the file executed
- where it came from
- its hash
- whether antivirus quarantined it
- whether other devices contain the same file

Do not execute an unknown file on your own workstation.

## 6. Example 5 — New Administrator Account

```text
Event ID: 4720
New account: backup_admin
Time: 02:17
```

Later, the account receives administrative privileges.

Questions include:

- who created it
- whether a change was approved
- where the action came from
- whether the account logged on later
- which systems it accessed

## 7. Example 6 — Suspicious SSH Activity

```text
Failed password for admin from 198.51.100.24
Failed password for admin from 198.51.100.24
Accepted password for admin from 198.51.100.24
```

Check whether:

- the IP is known
- external SSH is allowed
- the administrator recognises the session
- sudo was used
- cron jobs were created
- external connections followed

## 8. Example 7 — CTI Match

A trusted CTI source reports:

```text
malicious-example.com
```

as part of an active phishing campaign.

The SOC can ask:

```text
Have we seen this domain
inside our environment?
```

Search:

- DNS
- proxy
- firewall
- email gateway
- EDR
- SIEM

External intelligence now becomes an internal investigation.

## 9. Example 8 — Possible Ransomware

Users report:

```text
Documents no longer open.
File names have changed.
```

EDR shows mass file modification on several systems.

This may require rapid escalation.

Questions include:

- how many devices are affected
- whether the same process is involved
- whether a common account was used
- whether a ransom note exists
- whether file servers are affected
- whether backups are available

## 10. Example 9 — Repeated External Connection

```text
Source: workstation-24
Destination: 203.0.113.90
Port: 443
Connection every 60 seconds
```

Port 443 is commonly used for HTTPS and is not suspicious by itself.

Regular repeated communication may deserve investigation.

Check:

- the responsible process
- reputation of the IP or domain
- frequency
- whether other systems show the same pattern
- whether malware alerts exist

Regular callback behaviour is sometimes called beaconing.

## 11. Example 10 — False Positive

```text
Impossible travel detected
Budapest → London
20 minutes
```

Investigation shows that the user is in Budapest but uses a corporate VPN whose exit point is in London.

Assessment:

```text
False positive
```

Context changes the meaning of the alert.

## 12. Example 11 — Benign True Positive

A detection identifies repeated vulnerability scanning.

The source is the organisation's approved security scanner.

The rule correctly detected the behaviour, but the activity was authorised.

This may be classified as a benign true positive.

## 13. Example 12 — Missing Data Source

Dashboard:

```text
Windows Security logs
Last event received: 9 hours ago
```

No security alert exists, but this is still important.

Without logs, the SIEM has a detection blind spot.

Check collectors, network connectivity, storage, and recent configuration changes.

## 14. Simple Incident Note

```text
Alert:
Multiple failed logons followed by successful logon

User:
anna

Source IP:
198.51.100.24

Timeline:
09:01–09:04 — 18 failed logons
09:05 — successful logon

Assessment:
Suspicious activity, not yet confirmed malicious

Next step:
Contact user and review post-logon activity
```

A good note is short, factual, chronological, and separates facts from assumptions.

## 15. Entities

SIEM platforms often represent important investigation objects as **entities**.

Examples include:

- users
- computers
- IP addresses
- domains
- files
- processes

Connections between entities help build the story of an incident.

## 16. From Alert to Incident

One alert may represent one detected issue.

An incident may contain several related alerts and pieces of evidence.

Example:

```text
Alert 1 — suspicious login
Alert 2 — PowerShell activity
Alert 3 — malware detection
```

If they affect the same user and device, they may belong to one incident.

Microsoft Sentinel similarly treats incidents as collections of relevant alerts and evidence for an investigation.

## 17. Simple Prioritisation

Compare:

### Alert A

```text
1 failed logon
standard user
internal network
```

### Alert B

```text
successful external logon
domain admin account
nighttime
followed by PowerShell
```

Alert B should probably be investigated first because the account, access, timing, and related activity create greater potential risk.

## 18. Simple ATT&CK Mapping

```text
Phishing email
↓
PowerShell
↓
Scheduled Task
↓
External C2
```

Possible mapping:

| Event | ATT&CK |
|---|---|
| phishing | Initial Access |
| PowerShell | Execution |
| scheduled task | Persistence |
| C2 communication | Command and Control |

Mapping organises behaviour but does not replace evidence.

## 19. Simple Detection Tuning

Initial rule:

```text
Alert on every Event ID 4625
```

Result:

```text
3000 alerts per day
```

Improved rule:

```text
At least 15 Event ID 4625 events
for the same user
within 5 minutes
```

Result:

```text
8 alerts per day
```

The new version must still be tested to ensure real attacks are not missed.

## 20. Simple Threat Hunting

A hunt may start from a hypothesis instead of an alert.

Example:

```text
Attackers may be using
encoded PowerShell commands.
```

Questions:

- where did PowerShell run
- which commands contain EncodedCommand
- what was the parent process
- did external connections occur
- does the same pattern appear elsewhere

Threat hunting is proactive investigation.

## 21. CTI and Hunting

A CTI report may say that a relevant group often uses:

- phishing
- PowerShell
- scheduled tasks

Instead of searching only for one IP address, the SOC may look for a behavioural chain:

```text
Office → PowerShell → Scheduled Task
```

Behaviour-based searches can remain useful after individual indicators change.

## 22. How Should a Beginner Think?

A useful checklist is:

```text
1. What happened?
2. Why did the system alert?
3. What is normal?
4. What is unusual?
5. Which other data source can help?
6. What happened before?
7. What happened after?
8. What is a proven fact?
9. What is only an assumption?
10. What is the next step?
```

This way of thinking is more important than memorising a large number of commands.

## 23. Safe Practice

Good beginner activities include:

- analysing prepared logs
- using training SIEM environments
- searching test data
- using blue-team labs
- mapping examples to ATT&CK
- writing incident notes

Do not investigate systems without authorisation or run unknown malware on a normal workstation.

## 24. Mini Exercise 1

```text
18:01 — user1 failed login
18:01 — user1 failed login
18:02 — user1 failed login
18:04 — user1 successful login
18:06 — user1 created new account
```

Questions:

1. Which event is most important?
2. What makes the timeline suspicious?
3. Which additional data would you request?
4. Would you escalate?

## 25. Mini Exercise 2

```text
09:10 — outlook.exe
09:11 — winword.exe
09:12 — powershell.exe
09:12 — connection to 203.0.113.80
09:13 — new executable in Temp
```

Questions:

1. Which possible story does this sequence suggest?
2. What could be a normal explanation?
3. What would you inspect in PowerShell data?
4. Which ATT&CK tactics may apply?
5. Which EDR evidence would you search?

## 26. Mini Exercise 3

```text
02:10 — SSH failed
02:10 — SSH failed
02:11 — SSH successful
02:13 — sudo
02:15 — cron job created
```

Questions:

1. Why is the successful SSH session interesting?
2. What would you check around sudo?
3. Why may the cron job matter?
4. Which containment action might be required if compromise is confirmed?

## 27. Key Points for Beginners

- An alert is only the beginning of an investigation
- Always review events before and after the alert
- One event rarely proves an attack
- Context prevents incorrect conclusions
- Timelines are simple and very useful
- Facts and assumptions should be separated
- CTI can add context
- MITRE ATT&CK helps organise behaviour
- Detection tuning reduces noise
- Missing logs can create a security blind spot
- Good analysts know when to continue investigating and when to escalate
- Good questions are more important than memorising many technical commands

## 28. Review Questions

1. What should be the first question when reviewing an alert?
2. Why is a timeline useful?
3. Why do repeated failed logons not prove an attack?
4. Why may Word launching PowerShell be interesting?
5. How can a malware hash be used?
6. Why may a new administrator account matter?
7. What should be checked after a successful SSH logon?
8. How can a CTI indicator be used?
9. Why should ransomware suspicion be escalated quickly?
10. What is beaconing?
11. Why may impossible travel be a false positive?
12. What is a benign true positive?
13. Why is a failed log source a security problem?
14. What should an incident note contain?
15. What is an entity?
16. How do alerts and incidents differ?
17. What factors influence prioritisation?
18. What is ATT&CK mapping used for?
19. Why should detection rules be tuned?
20. What is threat hunting?

## References

1. Microsoft Learn  
   **Security incident management in Microsoft Sentinel**  
   https://learn.microsoft.com/en-us/training/modules/incident-management-sentinel/

2. Microsoft Learn  
   **Investigate Microsoft Sentinel incidents in depth**  
   https://learn.microsoft.com/en-us/azure/sentinel/investigate-incidents

3. Microsoft Learn  
   **Navigate, triage, and manage Microsoft Sentinel incidents**  
   https://learn.microsoft.com/en-us/azure/sentinel/incident-navigate-triage

4. Microsoft Learn  
   **Use tasks to manage incidents in Microsoft Sentinel**  
   https://learn.microsoft.com/en-us/azure/sentinel/incident-tasks

5. MITRE ATT&CK  
   **Get Started**  
   https://attack.mitre.org/resources/

6. MITRE ATT&CK  
   **Adversary Emulation Plans**  
   https://attack.mitre.org/resources/adversary-emulation-plans/

7. Hungarian National Cyber Security Center  
   **Incidenskezelés** [Hungarian]  
   https://nki.gov.hu/szolgaltatasok/tartalom/incidenskezeles/

8. Hungarian National Cyber Security Center  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

---

[← Previous chapter](12-detection-engineering.md) | [Back to contents](README.md) | [Next chapter →](14-cheat-sheet.md)
