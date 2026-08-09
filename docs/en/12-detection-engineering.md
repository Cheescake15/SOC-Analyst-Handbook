# 12 — Detection Engineering

[← Back to the English contents](README.md) | [Magyar változat](../hu/12-detection-engineering.md)

## Introduction

Previous chapters introduced logs, SIEM, MITRE ATT&CK, and incident response.

A natural next question is:

```text
How do raw logs become useful security alerts?
```

This is one of the main goals of **detection engineering**.

Detection engineering is the process of designing, testing, improving, and maintaining security detections.

The goal is to recognise important attacker behaviour without creating an unmanageable number of false alerts.

## 1. What Is a Detection?

A **detection** identifies a defined or unusual pattern in security data.

Example:

```text
One user produces
30 failed logons
within 5 minutes.
```

A rule may say:

```text
If one user has at least
30 failed logons in 5 minutes,
create an alert.
```

This activity may indicate brute force, although normal explanations are also possible.

## 2. What Is Detection Engineering?

Detection engineering normally includes:

1. understanding the threat
2. selecting the required data source
3. writing detection logic
4. testing the rule
5. reviewing false positives
6. tuning the rule
7. documenting it
8. reviewing it later

A good detection should be understandable and maintainable as well as technically functional.

## 3. Start With a Question

Before writing a query, define what you want to identify.

Example:

```text
How could we identify
unusual PowerShell activity?
```

Then ask:

- which PowerShell events are available
- which fields exist
- what is normal
- what is unusual
- which attacker behaviour matters

If the question is unclear, the detection logic will usually be unclear as well.

## 4. The Right Data Source

You can only detect activity that produces useful data.

For suspicious PowerShell use, relevant sources may include:

- Windows Event Logs
- PowerShell logs
- EDR telemetry
- process creation events
- network logs

If the required logging is missing, the rule cannot work.

```text
No data → no detection
```

Good event logging is therefore a basic requirement for threat detection.

## 5. Useful Fields

A detection may use:

- timestamp
- user name
- computer name
- source IP
- destination IP
- process name
- command line
- file name
- hash
- event ID
- service name

Example:

```text
ProcessName = powershell.exe
CommandLine contains "-EncodedCommand"
```

## 6. Simple and Complex Rules

### Simple Rule

Looks for one event.

```text
A new administrator account was created.
```

### Complex Rule

Connects several events.

```text
Many failed logons
AND
successful logon
AND
administrative privilege use
```

Complex rules may be more accurate, but they are harder to test and maintain.

Beginners should start with simpler logic.

## 7. Thresholds

Many detections use a threshold.

Example:

```text
10 failed logons in 5 minutes
```

Here:

```text
10 = threshold
5 minutes = time window
```

A threshold that is too low may create too many alerts.

A threshold that is too high may miss attacks.

## 8. Baselines

A **baseline** describes normal behaviour.

Examples:

- an administrator regularly uses PowerShell
- a finance user almost never does
- a server communicates at night
- a workstation is normally active only during working hours

Understanding normal behaviour makes unusual behaviour easier to recognise.

## 9. False Positives

A **false positive** is an alert caused by legitimate activity.

Example:

```text
The rule alerts because
PowerShell was used.

The IT team was performing
approved maintenance.
```

Too many false positives can contribute to alert fatigue.

## 10. False Negatives

A **false negative** occurs when malicious activity happens but the detection misses it.

Example:

```text
The rule only searches
for powershell.exe.

The attacker starts PowerShell
through another mechanism.
```

False negatives can be more difficult to discover than false positives.

## 11. Tuning

**Tuning** means improving detection logic.

Initial rule:

```text
Alert on every PowerShell launch.
```

Improved rule:

```text
Alert when PowerShell
uses encoded commands,
downloads content,
or starts from an Office application.
```

The goal is to reduce noise while preserving useful detection.

## 12. Rule Lifecycle

A simple lifecycle is:

```text
Idea
 ↓
Development
 ↓
Testing
 ↓
Deployment
 ↓
Monitoring
 ↓
Tuning
 ↓
Review
 ↓
Update or retirement
```

Detections must change as systems and attacker behaviour change.

## 13. Testing

Before deployment, check:

- whether the detection finds the intended event
- how often it runs
- how much data it searches
- how many results it produces
- which false positives occur
- whether required fields exist

Testing helps reveal limitations before analysts depend on the rule.

## 14. Documentation

Useful rule documentation includes:

- rule name
- purpose
- reason for the detection
- data source
- required fields
- ATT&CK technique
- expected false positives
- severity
- analyst investigation steps

Microsoft Sentinel analytics rules also separate fields such as name, description, severity, ATT&CK mapping, and query logic.

## 15. MITRE ATT&CK and Detection Engineering

ATT&CK can help organise detection work.

Example technique:

```text
T1059.001 — PowerShell
```

Questions include:

- which data source can observe it
- what behaviour would be suspicious
- whether a rule already exists
- where detection gaps exist

## 16. Detection Coverage

**Detection coverage** describes which attacker behaviours the organisation can detect.

However:

```text
Rule exists ≠ reliable detection
```

A rule may be poorly configured, too narrow, noisy, or outdated.

Coverage should therefore be validated.

## 17. What Is Sigma?

**Sigma** is an open format for describing log-based detection rules.

It can be thought of as a common language for detections.

Sigma rules are written as YAML text files.

A rule can be converted into queries for different SIEM platforms, including:

- Microsoft Sentinel
- Splunk
- Elasticsearch
- Grafana Loki

This makes detection logic more portable and less tied to one vendor.

## 18. A Simple Sigma Example

Simplified example:

```yaml
title: Multiple Failed Windows Logons

logsource:
  product: windows
  service: security

detection:
  selection:
    EventID: 4625
  condition: selection

level: medium
```

This searches for Windows Event ID 4625, which represents a failed logon.

It is not yet a complete high-quality detection because one failed logon is usually normal.

Real rules may add time windows, counts, or other conditions.

## 19. Main Parts of a Sigma Rule

### title

The rule name.

### logsource

Which logs should be searched.

### detection

What the rule looks for.

### condition

When the detection matches.

### falsepositives

Expected legitimate causes.

### level

Estimated severity.

### tags

May include MITRE ATT&CK references.

Sigma documentation describes detection, logsource, and metadata as core rule components.

## 20. Vendor-Neutral Thinking

It is useful to define the behaviour before choosing a query language.

Instead of asking:

```text
Which KQL query should I write?
```

Ask:

```text
Which attacker behaviour
do I want to identify?

Which data would prove it?
```

Then implement the idea in KQL, SPL, Sigma, or another language.

## 21. Simple Detection Engineering Example

### Goal

Detect suspicious PowerShell use.

### Hypothesis

Encoded PowerShell is unusual for normal users.

### Required Data

```text
ProcessName
CommandLine
User
Computer
Timestamp
ParentProcess
```

### First Logic

```text
ProcessName = powershell.exe
AND
CommandLine contains EncodedCommand
```

### Test

Search the previous 30 days.

### Result

250 events are found.

230 are generated by an approved administration tool.

### Tuning

Exclude the precisely identified approved process.

### New Result

20 events remain.

These are more realistic for manual review.

## 22. What Should an Analyst Check After an Alert?

A suspicious PowerShell alert may require checking:

1. which user ran it
2. which device was involved
3. which command ran
4. the parent process
5. external network connections
6. newly created files
7. similar activity on other devices
8. related CTI information

A detection becomes more useful when investigation guidance is included.

## 23. Detection Maintenance

Review a rule when:

- it produces too many alerts
- it has never alerted for months
- the data source changed
- new software was introduced
- attacker behaviour changed
- a new ATT&CK technique became important
- analysts routinely ignore the alert

Old rules should not automatically be assumed to remain useful.

## 24. What Should We Avoid?

Poor practices include:

- alerting on every event
- writing rules without understanding the threat
- depending on unavailable fields
- adding unlimited exclusions
- deploying without testing
- never reviewing rules
- adding ATT&CK tags without real mapping

The goal is not to maximise the number of rules.

The goal is useful detection capability.

## 25. Key Points for Beginners

- Detection engineering designs and improves security detections.
- Start by understanding attacker behaviour.
- Detection requires suitable data.
- Thresholds and time windows are common rule elements.
- A baseline describes normal behaviour.
- A false positive is an incorrect alert.
- A false negative is missed malicious activity.
- Tuning improves detection quality.
- Rules should be tested and documented.
- MITRE ATT&CK can organise detection coverage.
- Sigma is an open vendor-neutral detection format.
- Detection engineering is a continuous process.

## 26. Review Questions

1. What is detection engineering?
2. What is a detection rule?
3. Why should you start with a clear question?
4. Why is the data source important?
5. What is a threshold?
6. What is a time window?
7. What is a baseline?
8. What is a false positive?
9. What is a false negative?
10. What is tuning?
11. What is the rule lifecycle?
12. Why should detections be tested?
13. What should rule documentation contain?
14. How can MITRE ATT&CK help?
15. What is detection coverage?
16. What is Sigma?
17. Why is Sigma vendor-neutral?
18. What is the role of logsource?
19. Why should investigation guidance accompany an alert?
20. Why should rules be reviewed regularly?

## References

1. Microsoft Learn  
   **Create and publish analytics rules for Microsoft Sentinel solutions**  
   https://learn.microsoft.com/en-us/azure/sentinel/isv/sentinel-analytic-rules-creation

2. Microsoft Learn  
   **Scheduled analytics rules in Microsoft Sentinel**  
   https://learn.microsoft.com/en-us/azure/sentinel/scheduled-rules-overview

3. Microsoft Learn  
   **Create scheduled analytics rules in Microsoft Sentinel**  
   https://learn.microsoft.com/en-us/azure/sentinel/create-analytics-rules

4. MITRE ATT&CK  
   **Data Sources**  
   https://attack.mitre.org/datasources/

5. Sigma Detection Format  
   **Getting Started**  
   https://sigmahq.io/docs/

6. Sigma Detection Format  
   **Sigma Rules**  
   https://sigmahq.io/docs/basics/rules.html

7. Hungarian National Cyber Security Center  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

8. Gyaraki Réka, editor  
   **Az információbiztonság alapjai** [Hungarian]  
   National University of Public Service, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Previous chapter](11-malware-basics.md) | [Back to contents](README.md) | [Next chapter →](13-practical-examples.md)
