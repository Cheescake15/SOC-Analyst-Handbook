# 02 — How a SOC Works

[← Back to the English contents](README.md) | [Magyar változat](../hu/02-how-a-soc-works.md)

## Introduction

This chapter gives a beginner-level overview of how a Security Operations Center operates. It focuses on the main roles, processes, data sources, and technologies without assuming professional SOC experience.

The sources suggest that an effective SOC relies on three connected areas: people, processes, and technology.

A Hungarian National Cyber Security Center article on incident-handling platforms notes that such platforms can support the work of SOC, CSIRT, and CERT teams during investigations. This is a useful reminder that technology supports the investigation process rather than replacing analyst judgement.

## 1. People, Processes, and Technology

### People

A SOC may include:

- Tier 1 analysts
- Tier 2 investigators
- senior analysts
- threat hunters
- detection engineers
- incident responders
- SOC engineers
- SOC managers

In smaller organisations, one person may perform several of these functions.

### Processes

Processes explain how the team should handle an alert or incident.

Examples include:

- initial alert review
- escalation rules
- evidence collection
- ticket documentation
- shift handover
- containment approval

### Technology

Common SOC tools include:

- SIEM
- EDR and XDR
- IDS and IPS
- firewalls
- email security platforms
- threat intelligence platforms
- SOAR
- ticketing systems

These tools organise data, but human analysis is still needed.

## 2. SOC Data Sources

A SOC may use:

- Windows Event Logs
- Linux authentication logs
- firewall logs
- DNS logs
- VPN logs
- Active Directory events
- endpoint telemetry
- cloud audit logs
- email security events
- application logs

A single event is often not enough to make a decision. Analysts may compare several sources.

## 3. From Event to Alert

Systems generate many normal events.

An alert may be created when activity matches a detection rule.

```text
If a user has 20 failed logins within 10 minutes
and then logs in successfully,
create an alert.
```

An alert does not prove that an attack occurred. It means that the activity may require investigation.

## 4. Typical Alert Lifecycle

```text
Event
  ↓
Detection
  ↓
Alert
  ↓
Initial review
  ↓
Context collection
  ↓
Classification
  ↓
Closure or escalation
```

During triage, an analyst may ask:

- How urgent is the case?
- Is a critical system involved?
- Is the activity unusual for the user?
- Is deeper investigation required?

Possible classifications include:

- true positive
- benign true positive
- false positive
- informational
- further investigation required

## 5. Priority and Severity

Priority may depend on:

- the affected asset
- user privileges
- possible business impact
- data sensitivity
- whether the threat is still active
- the number of affected systems

The same alert may receive a different priority depending on the context.

## 6. Playbooks and Runbooks

A playbook describes the main steps for handling an event type.

A runbook may contain detailed technical instructions.

For example:

- which SIEM query to run
- how to isolate an endpoint
- which ticket fields to complete

## 7. Escalation

Escalation may be needed when:

- a critical system is affected
- a privileged account is involved
- several systems may be compromised
- data loss is suspected
- the case exceeds the analyst's authority
- immediate action may be required

## 8. Cooperation with Other Teams

A SOC may work with:

- IT operations
- Identity and Access Management
- legal
- privacy
- human resources
- communications
- management

The SOC should explain both the technical facts and the possible business impact.

## 9. Shift Handover

A useful handover may include:

- open alerts
- active incidents
- completed steps
- remaining tasks
- ticket numbers
- deadlines

Example:

```text
Suspicious PowerShell activity was detected on WS-104 at 22:14.
The EDR investigation has started.
The endpoint has not yet been isolated.
Next step: review the process tree and network connections.
Ticket: INC-2481.
```

## 10. Automation

SOAR and other tools may automate:

- IP reputation checks
- hash checks
- ticket creation
- notifications
- email quarantine

High-impact actions may still require human approval.

## 11. Performance Metrics

Common metrics include:

- Mean Time to Detect
- Mean Time to Acknowledge
- Mean Time to Respond
- Mean Time to Contain
- False Positive Rate
- Alert Volume

These metrics can support improvement, but they do not provide a complete view on their own.

## Chapter Summary

A SOC combines people, processes, and technology.

Analysts review alerts, collect context, assess risk, document findings, and escalate when necessary.


## References

1. NIST SP 800-61 Rev. 3  
   https://csrc.nist.gov/pubs/sp/800/61/r3/final

2. NIST Cybersecurity Framework 2.0  
   https://www.nist.gov/cyberframework

3. CISA Cybersecurity Incident and Vulnerability Response Playbooks  
   https://www.cisa.gov/news-events/news/cisa-releases-updated-cybersecurity-incident-and-vulnerability-response-playbooks

4. MITRE ATT&CK Data Sources  
   https://attack.mitre.org/datasources/

5. Hungarian National Cyber Security Center  
   **Incidenskezelési platformok** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/tanacsok/incidenskezelesi-platformok/

6. Gyaraki Réka, editor  
   **Az információbiztonság alapjai** [Hungarian]  
   National University of Public Service, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf
