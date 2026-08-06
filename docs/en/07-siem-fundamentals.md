# 07 — SIEM Fundamentals

[← Back to the English contents](README.md) | [Magyar változat](../hu/07-siem-fundamentals.md)

## Introduction

The previous chapter explained how individual logs can be analysed. In a large organisation, many systems produce logs, so reviewing each one manually is not realistic.

A SIEM helps solve this problem.

SIEM stands for *Security Information and Event Management*.

In simple terms, a SIEM collects security data from different systems, makes it searchable, and may create alerts when it detects suspicious patterns.

## 1. A Simple Comparison

A SIEM can be compared to a central security control desk.

A large building may have separate systems for access cards, cameras, fire alarms, lifts, and emergency exits.

When all information appears in one place, it becomes easier to identify a sequence such as:

1. someone entered at night
2. they visited a restricted floor
3. an emergency exit opened soon afterwards

A SIEM connects computer events in a similar way.

## 2. Which Data Can a SIEM Collect?

Examples include:

- Windows logs
- Linux logs
- firewall logs
- VPN events
- DNS queries
- cloud logs
- antivirus alerts
- EDR data
- email security events
- application logs
- authentication records

Organisations select sources based on risk, cost, and investigation needs.

## 3. How Does Data Reach the SIEM?

```text
A system creates an event
        ↓
The log is forwarded
        ↓
The SIEM receives it
        ↓
Fields are processed
        ↓
The data becomes searchable
        ↓
Rules and queries can examine it
```

Data may arrive through:

- an installed agent
- network forwarding
- an API
- a cloud connector
- file import

An agent is a small program that collects and forwards data from a device or server.

## 4. Processing and Normalisation

Different systems use different log formats.

A SIEM may:

1. receive the data
2. recognise the format
3. extract fields
4. normalise field names
5. store the data

For example:

```text
src_ip
source_ip
client_ip
```

All may describe the source IP address.

Normalisation makes them easier to search consistently.

## 5. Searching in a SIEM

An analyst may ask:

```text
Which users had more than 10 failed logons
during the last hour?
```

Or:

```text
Which computers connected
to IP address 203.0.113.50?
```

Query languages differ by product.

Examples include:

- KQL in Microsoft Sentinel
- SPL in Splunk
- KQL or EQL in Elastic environments

For a beginner, the first skill is not memorising the full query language. It is learning to ask a clear question.

## 6. Detection Rules

A detection rule defines when the SIEM should create an alert.

Example:

```text
If one user has 20 failed logons
within 10 minutes,
create an alert.
```

A rule may combine several conditions:

```text
Many failed logons
AND
a successful logon
AND
an unknown external IP address
```

More conditions may improve accuracy, but an overly strict rule may miss real attacks.

## 7. Correlation

Correlation means looking for relationships between several events.

Example:

```text
VPN: successful external logon
Windows: PowerShell started
Firewall: connection to an unknown server
Active Directory: new administrator account
```

A SIEM may place these events on one timeline.

This helps analysts see a possible attack sequence instead of isolated records.

## 8. Event, Alert, and Incident

### Event

Something happened in a system.

```text
A user logged on.
```

### Alert

A rule or security tool marked the event as suspicious.

```text
The user logged on from an unusual country.
```

### Incident

One or more alerts were connected to a likely or confirmed security problem.

```text
The account was probably compromised.
```

Not every event becomes an alert, and not every alert becomes an incident.

## 9. Priority and Severity

SIEM alerts often receive labels such as:

- Low
- Medium
- High
- Critical

Severity may depend on:

- asset importance
- user privileges
- data sensitivity
- detection confidence
- related events
- possible business impact

A high-severity label does not prove an attack. It helps analysts decide which cases to review first.

## 10. Dashboards

A dashboard is an overview screen containing charts and tables.

It may show:

- alert volume
- common alert types
- failed logons
- active source IP addresses
- open incidents
- severity distribution
- data-source health

Dashboards provide a quick overview but do not replace detailed investigation.

## 11. Alert Fatigue

When a SIEM creates too many alerts, analysts may struggle to review them properly.

This is called alert fatigue.

Possible causes include:

- overly sensitive rules
- many false positives
- incorrectly configured sources
- duplicated alerts
- missing business context
- outdated rules

Possible improvements include:

- rule tuning
- careful exceptions
- alert grouping
- risk-based prioritisation
- regular review

The goal is not to create the highest possible number of alerts. The goal is to create useful alerts.

## 12. What Is Tuning?

Tuning means improving a detection rule.

A rule that alerts on every PowerShell launch may create too much noise.

It may be improved to alert when PowerShell:

```text
runs encoded commands,
downloads a file,
or starts from an Office application.
```

Exceptions must be used carefully so that real attacks are not hidden.

## 13. SIEM and SOAR

### SIEM

Main functions include:

- collecting data
- providing search
- correlating events
- creating alerts
- supporting investigations

### SOAR

SOAR stands for *Security Orchestration, Automation and Response*.

It may:

- perform automated steps
- run playbooks
- connect security tools
- speed up response actions

For example, the SIEM may create an alert about a malicious IP address, while the SOAR automatically checks its reputation and opens a ticket.

## 14. SIEM Limitations

A SIEM cannot solve every security problem.

It may fail when:

- important logs are missing
- clocks are not synchronised
- parsing is incorrect
- retention is too short
- rules are poorly configured
- alerts are not investigated
- business context is missing

In simple terms:

```text
A SIEM can only analyse
the data it actually receives.
```

## 15. Data Quality

Data quality matters as much as data volume.

Problems include:

- missing user names
- incorrect timestamps
- missing source IP addresses
- sources that stopped sending data
- incorrectly parsed fields
- duplicate events

A SOC should therefore monitor the health of its log sources.

## 16. Simple SIEM Example

The SIEM sees:

```text
10:01 — 25 failed logons
10:04 — successful logon
10:06 — PowerShell started
10:07 — connection to a bad-reputation IP
10:09 — new scheduled task
```

A detection rule creates a high-priority alert.

The analyst may then review:

1. which account is involved
2. where the connection came from
3. which PowerShell command ran
4. which process connected externally
5. what the scheduled task starts
6. whether similar activity appears elsewhere
7. whether the user recognises the activity

The SIEM collects and connects the evidence. The analyst makes the final assessment.

## 17. Key Points for Beginners

- A SIEM collects security data from many systems
- It makes data searchable and comparable
- Detection rules may create alerts
- Correlation connects related events
- Not every alert means an attack
- Too many alerts may cause alert fatigue
- Tuning improves detection rules
- SIEM and SOAR have different roles
- A SIEM depends on good data
- Human judgement is still necessary


## References

1. Microsoft Learn  
   **What is Microsoft Sentinel SIEM?**  
   https://learn.microsoft.com/en-us/azure/sentinel/overview

2. Microsoft Learn  
   **Design solutions for security operations**  
   https://learn.microsoft.com/en-us/training/modules/design-solutions-security-operations/

3. Cybersecurity and Infrastructure Security Agency  
   **Use Logging on Business Systems**  
   https://www.cisa.gov/audiences/small-and-medium-businesses/secure-your-business/use-logging-on-business-systems

4. Cybersecurity and Infrastructure Security Agency  
   **Enhanced Visibility and Hardening Guidance for Communications Infrastructure**  
   https://www.cisa.gov/resources-tools/resources/enhanced-visibility-and-hardening-guidance-communications-infrastructure

5. Hungarian National Cyber Security Center  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

6. Gyaraki Réka, editor  
   **Az információbiztonság alapjai** [Hungarian]  
   National University of Public Service, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Previous chapter](06-log-analysis.md) | [Back to contents](README.md) | [Next chapter →](08-cyber-threat-intelligence.md)
