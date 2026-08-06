# 06 — Log Analysis

[← Back to the English contents](README.md) | [Magyar változat](../hu/06-log-analysis.md)

## Introduction

Computers, servers, applications, and network devices continuously record what happens. These records are called logs.

A single log entry is often only a small piece of information. When several entries are placed in chronological order, they may tell a complete story.

This chapter explains log analysis at a beginner level. It focuses on useful fields, simple searches, timelines, and the importance of context.

## 1. What Is a Log?

A log is an automatically created record of an event.

It is similar to a digital diary kept by a system.

A log entry may show:

- when something happened
- which system was involved
- which user was involved
- which program ran
- whether an action succeeded
- which IP address was used

Example:

```text
2026-08-06 08:14:22
User: andrea
Action: Login
Result: Failed
Source IP: 203.0.113.24
```

## 2. Why Logs Matter

Logs may support:

- troubleshooting
- user activity review
- attack detection
- incident investigation
- timeline creation
- evidence preservation

CISA emphasise that effective logging is necessary to understand what happened in a system.

## 3. Common Log Sources

- Windows
- Linux
- firewalls
- routers
- VPN systems
- DNS servers
- web servers
- email systems
- antivirus products
- EDR platforms
- cloud services
- databases
- business applications

An investigation often requires several sources.

## 4. Important Log Fields

### Timestamp

```text
2026-08-06T08:14:22+02:00
```

The time zone matters. One system may use local time while another uses UTC.

### User

```text
User: admin
```

### Source and Destination

```text
Source IP: 198.51.100.17
Destination IP: 10.0.0.25
Destination Port: 22
```

### Event Type

```text
Login failed
File created
Service started
Connection blocked
```

### Result

```text
Result: Success
```

## 5. Structured and Unstructured Logs

### Structured Log

```json
{
  "time": "2026-08-06T08:14:22Z",
  "user": "andrea",
  "action": "login",
  "result": "failed",
  "source_ip": "203.0.113.24"
}
```

### Unstructured Log

```text
Failed password for andrea from 203.0.113.24 port 52311 ssh2
```

Structured data is usually easier to search.

## 6. What Is Normalisation?

Different systems may use different names for the same field.

```text
src_ip
source_ip
client_ip
remote_address
```

All may refer to the source IP address.

**Normalisation** converts them into a consistent format. SIEM platforms often perform this task.

## 7. Building a Timeline

```text
09:02 — failed logon
09:03 — failed logon
09:04 — successful logon
09:06 — file downloaded
09:08 — PowerShell started
09:10 — connection to an unknown external address
```

Separately, the entries may not prove an attack. Together, they form a sequence that deserves investigation.

## 8. Searching and Filtering

Useful filters include:

- time range
- user name
- IP address
- computer name
- event type
- error code
- process name
- port
- result

Example:

```text
Show failed logons for the admin account
during the last 24 hours.
```

A good search starts with a clear question.

## 9. What Looks Suspicious?

Suspicious does not mean proven malicious.

An event may deserve attention when it:

- is rare
- happens at an unusual time
- involves a privileged account
- uses an unknown IP address
- appears on several systems
- is followed by other unusual events

Context is always required.

## 10. True Positive and False Positive

### True Positive

The alert identifies a real security problem.

### False Positive

The alert identifies normal activity as suspicious.

### Benign True Positive

The detection correctly identifies the pattern, but the activity is authorised.

For example, an approved security test.

## 11. The Role of Context

Example:

```text
powershell.exe started
```

This may be:

- normal administration
- software installation
- a corporate script
- malicious activity

Useful questions include:

- who started it
- which device ran it
- which command was used
- what the parent process was
- whether it contacted an external address
- whether files changed

## 12. Time Synchronisation

If system clocks differ, events may appear in the wrong order.

Analysts should check:

- time zone
- whether the log uses UTC
- clock accuracy
- daylight-saving changes

Systems often use NTP for time synchronisation.

## 13. Log Retention and Protection

Retention may depend on:

- storage capacity
- laws and regulations
- internal policy
- business needs
- investigation requirements
- privacy requirements

Logs also need protection.

Useful controls include:

- central collection
- limited access
- backups
- change monitoring
- alerts when logging stops

Attackers may try to erase evidence, so unexpected logging failure may itself require investigation.

## 14. Simple Investigation Example

```text
14:21 — 15 failed VPN logons
14:24 — successful VPN logon
14:27 — Remote Desktop connection
14:30 — new administrator account
14:34 — logging service stopped
```

A beginner analyst may ask:

1. which user is involved
2. where the connection came from
3. whether the user recognises it
4. who created the new account
5. which privileges were assigned
6. what stopped logging
7. whether similar events occurred elsewhere

## 15. A Simple Analysis Method

1. Define the question.
2. Define the time range.
3. Collect identifiers.
4. Find related events.
5. Build a timeline.
6. Separate known and unknown facts.
7. Document the conclusion and next step.

## 16. Key Points for Beginners

- A log is a system-created event record.
- One entry rarely gives the full picture.
- Timestamps and time zones are important.
- Several sources may need to be connected.
- Unusual activity is not automatically malicious.
- Context supports correct interpretation.
- Logs must be retained and protected.
- A simple timeline can make an investigation much clearer.


## References

1. Cybersecurity and Infrastructure Security Agency  
   **Use Logging on Business Systems**  
   https://www.cisa.gov/audiences/small-and-medium-businesses/secure-your-business/use-logging-on-business-systems

2. Microsoft Learn  
   **Event Viewer**  
   https://learn.microsoft.com/en-us/shows/inside/event-viewer

3. Microsoft Learn  
   **Windows Event Log**  
   https://learn.microsoft.com/en-us/windows/win32/wes/windows-event-log

4. Hungarian National Cyber Security Center  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

5. Gyaraki Réka, editor  
   **Az információbiztonság alapjai** [Hungarian]  
   National University of Public Service, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Previous chapter](05-linux-security.md) | [Back to contents](README.md) | [Next chapter →](07-siem-fundamentals.md)
