# 02 — How a SOC Works

[← Back to the English contents](README.md) | [Magyar változat](../hu/02-how-a-soc-works.md)

## Introduction

A Security Operations Center is often imagined as a room full of screens where analysts watch attacks in real time. The reality is more complex. A functioning SOC is not simply a collection of security products. It is a coordinated system of people, processes, and technology.

The SOC does not treat every alert as an incident. Its job is to identify the events that may represent real risk, investigate them efficiently, and coordinate an appropriate response.

## 1. The Three Foundations of a SOC

Most SOC operating models rely on three foundations:

- people
- processes
- technology

None of them works effectively in isolation.

### People

Analysts interpret alerts, connect information from different sources, make decisions, and document their findings.

A SOC may include:

- Tier 1 analysts
- Tier 2 investigators
- senior analysts
- threat hunters
- detection engineers
- incident responders
- SOC engineers
- SOC managers

### Processes

Processes define what the team should do in a specific situation.

They may describe:

- alert prioritisation
- escalation rules
- evidence collection
- ticket handling
- shift handovers
- management notification
- containment approval

### Technology

Common SOC technologies include:

- SIEM
- EDR and XDR
- IDS and IPS
- firewalls
- email security platforms
- vulnerability management systems
- threat intelligence platforms
- SOAR
- ticketing systems
- cloud security services

Tools assist the analyst, but they do not replace professional judgement.

## 2. Where Does the Data Come From?

Common sources include:

- Windows Event Logs
- Linux system and authentication logs
- firewall logs
- DNS logs
- proxy and web logs
- VPN logs
- Active Directory events
- endpoint telemetry
- email security events
- cloud audit logs
- application logs
- network traffic data

### Example

A single failed login is not necessarily suspicious. Hundreds of failed attempts from one IP address followed by a successful login may require immediate investigation.

The analyst may correlate:

- authentication logs
- VPN records
- IP reputation
- user history
- endpoint activity
- multi-factor authentication events

## 3. How Does an Event Become an Alert?

Systems continuously generate events. Most of them are part of normal operations.

A detection rule or analytical model creates an alert when an event or sequence of events matches a defined condition.

```text
If a user has at least 20 failed logins
within 10 minutes,
followed by a successful login,
create a high-priority alert.
```

This does not prove that an attack occurred. It indicates that the activity deserves investigation.

## 4. The Alert Lifecycle

```text
Data is generated
      ↓
Detection logic identifies a pattern
      ↓
An alert is created
      ↓
Tier 1 triage
      ↓
Context collection
      ↓
Classification
      ↓
Closure or escalation
      ↓
Incident response
      ↓
Review and improvement
```

### Triage

Triage is a rapid first assessment.

The analyst tries to determine:

- whether there may be a real security risk
- how urgent the case is
- whether deeper investigation is required
- whether immediate action is needed
- whether the case should be transferred

### Context Collection

Typical questions include:

- Is the IP address known?
- Is the location normal for the user?
- Which process was executed?
- What was the parent process?
- Was a file downloaded?
- Are there related alerts?
- Is a privileged account involved?
- Is similar activity visible on other systems?

### Classification

The analyst may classify the alert as:

- true positive
- benign true positive
- false positive
- informational
- requiring further investigation

## 5. Priority and Severity

Analysts may consider:

- the affected asset
- business criticality
- user privileges
- potential impact
- detection confidence
- whether the threat is still active
- whether sensitive data is involved
- how widely the activity has spread

## 6. Playbooks and Runbooks

A playbook describes the overall response to a type of event.

A runbook provides more detailed execution instructions.

The important point is that analysts follow repeatable and understandable procedures.

## 7. Escalation

Escalation does not mean that an analyst has failed. A capable analyst knows when another specialist or decision-maker must become involved.

Examples of technical escalation:

- malware analyst
- incident responder
- digital forensics specialist
- cloud security specialist
- identity specialist

Management may need to become involved when:

- there may be major business impact
- regulatory obligations apply
- personal data may be affected
- a communication decision is required

## 8. Cooperation with Other Teams

A SOC cannot operate in isolation.

Common partners include:

- IT operations
- Identity and Access Management
- legal
- privacy
- human resources
- communications
- business owners
- management

## 9. Shift Handover

A useful handover includes:

- open alerts
- active incidents
- completed actions
- remaining tasks
- important deadlines
- relevant contacts
- known technical problems
- temporarily modified detections

### Weak Handover

```text
Please check the suspicious PowerShell alert.
```

### Better Handover

```text
Encoded PowerShell activity was detected on endpoint WS-104 at 22:14.
The user confirmed that no administrative work was performed.
An EDR investigation has started.
The endpoint has not yet been isolated.
Next step: review the process tree and network connections.
Ticket: INC-2481.
```

## 10. Automation in the SOC

Examples include:

- checking IP reputation
- checking file hashes
- collecting user information
- creating tickets
- quarantining email
- isolating endpoints
- sending notifications

High-impact actions often require human approval.

## 11. Measuring SOC Performance

Common examples include:

- Mean Time to Detect
- Mean Time to Acknowledge
- Mean Time to Respond
- Mean Time to Contain
- False Positive Rate
- Escalation Rate
- Alert Volume

Metrics must be interpreted carefully. Closing alerts quickly does not necessarily mean that investigations are accurate.

## 12. Practical Example

A finance employee's account signs in from several countries within a short period.

The analyst reviews:

- IP addresses
- login times
- device identifiers
- multi-factor authentication events
- previous user behaviour
- activity after login

Possible explanations include VPN use, travel, inaccurate geolocation, stolen credentials, or a stolen session token.

If the user does not recognise the activity and the login is followed by unusual file downloads or mailbox rule creation, the case should be escalated.

## 13. Chapter Summary

A SOC depends on the coordination of people, processes, and technology.

Alert handling involves more than clicking a closure button. Analysts must understand context, assess risk, document their work, and escalate when needed.

## 14. Review Questions

1. What are the three foundations of a SOC?
2. Why is a SIEM not sufficient by itself?
3. What is the difference between an event and an alert?
4. What does triage mean?
5. Which factors influence alert priority?
6. What is the difference between a playbook and a runbook?
7. When is technical escalation necessary?
8. Which teams may cooperate with the SOC?
9. What should a useful shift handover contain?
10. What are the benefits and risks of automation?

## References

1. NIST SP 800-61 Rev. 3  
   https://csrc.nist.gov/pubs/sp/800/61/r3/final

2. NIST Cybersecurity Framework 2.0  
   https://www.nist.gov/cyberframework

3. CISA Cybersecurity Incident and Vulnerability Response Playbooks  
   https://www.cisa.gov/news-events/news/cisa-releases-updated-cybersecurity-incident-and-vulnerability-response-playbooks

4. MITRE ATT&CK Data Sources  
   https://attack.mitre.org/datasources/

---

[← Previous chapter](01-introduction.md) | [Back to contents](README.md) | [Next chapter →](03-network-fundamentals.md)
