# 01 — Introduction to Security Operations

[← Back to the English contents](../../README.md) | [Magyar változat](../hu/01-introduction.md)

## Chapter Objectives

This chapter introduces the role of a Security Operations Center (SOC), the fundamental responsibilities of a blue team, the typical duties of SOC analysts, and the differences between common analyst levels.

By the end of this chapter, readers should be able to:

- define a SOC and explain why organisations need one
- distinguish between blue team and red team activities
- describe the core responsibilities of a SOC analyst
- differentiate Tier 1, Tier 2, and Tier 3 roles
- explain the difference between a NOC and a SOC
- outline the typical lifecycle of a security alert

---

## 1. What Is a Security Operations Center?

A **Security Operations Center**, commonly abbreviated as **SOC**, is an organisational function or specialist team that continuously monitors, analyses, and protects an organisation’s information technology environment.

In NIST terminology, a SOC is a central component of an organisation’s security operations. In practice, the SOC collects and analyses data from different security tools and systems, then responds to suspicious or harmful activity.

A SOC may monitor:

- workstations and laptops
- servers
- network devices
- cloud services
- user accounts
- business applications
- endpoint security platforms
- firewalls and intrusion detection systems
- security information and event management platforms

A SOC does not necessarily refer to a single physical room. It may operate as:

- an internal organisational unit
- a geographically distributed team
- a fully remote team
- an outsourced service
- a hybrid model

Outsourced monitoring is often provided by a **Managed Security Service Provider** (MSSP) or a **Managed Detection and Response** (MDR) provider.

---

## 2. Why Do Organisations Need a SOC?

Modern organisations operate large numbers of devices, applications, user accounts, networks, and cloud services. These systems continuously generate logs and security events.

A single security tool cannot normally provide a complete view of the organisation’s security posture. The SOC brings together information from multiple sources, adds context, and prioritises the events that require attention.

The main objectives of a SOC include:

1. **Continuous monitoring**  
   Reviewing security-relevant activity across the environment.

2. **Threat detection**  
   Identifying suspicious behaviour, attack patterns, and signs of compromise.

3. **Alert investigation**  
   Determining whether an alert represents a real threat or an incorrect detection.

4. **Incident response**  
   Supporting the containment of damage, interruption of attacker activity, and recovery of affected systems.

5. **Security visibility**  
   Providing technical teams and management with an understanding of the organisation’s security posture.

6. **Continuous improvement**  
   Using lessons from previous events to improve monitoring, processes, and controls.

The NIST Cybersecurity Framework 2.0 defines six high-level Functions:

- **Govern**;
- **Identify**;
- **Protect**;
- **Detect**;
- **Respond**;
- **Recover**.

SOC work is especially closely associated with Detect, Respond, and Recover. However, an effective SOC also depends on governance, asset knowledge, risk management, and preventive controls.

---

## 3. What Is a Blue Team?

The **blue team** represents the defensive side of cybersecurity. Its purpose is to protect systems, detect attacks, respond to incidents, and improve the organisation’s security capabilities.

Blue team activities may include:

- monitoring security events
- analysing logs
- investigating alerts
- responding to incidents
- protecting endpoints and networks
- supporting vulnerability management
- using cyber threat intelligence
- developing detections
- conducting threat hunting
- validating security controls
- preparing reports and documentation

The blue team is not necessarily identical to the SOC. The SOC is usually a central part of blue team operations, but the broader defensive function may also include:

- security engineers
- incident responders
- malware analysts
- digital forensics specialists
- cyber threat intelligence analysts
- cloud security specialists
- vulnerability management specialists

### Blue Team and Red Team

A **red team** uses authorised attacker-like techniques to test the organisation’s defences. The **blue team** attempts to prevent, detect, investigate, and respond to those activities.

Their ultimate objective is shared: improving the organisation’s security.

| Blue Team | Red Team |
|---|---|
| Focuses on defence | Simulates attacker behaviour |
| Analyses alerts and logs | Searches for and exploits weaknesses |
| Responds to incidents | Tests defensive controls |
| Develops detections | Attempts to evade detections |
| Performs continuous defensive work | Usually operates during defined engagements |

Structured cooperation between the two sides is often called **purple teaming**.

---

## 4. Responsibilities of a SOC Analyst

The primary responsibility of a SOC analyst is to investigate security events and identify activity that may threaten the organisation.

Daily work varies between organisations, but commonly includes the following areas.

### 4.1 Alert Triage

During **triage**, the analyst quickly assesses:

- what triggered the alert
- which system or user is involved
- how urgent the event may be
- whether the activity may be malicious
- whether further investigation or escalation is required

### 4.2 Log and Telemetry Analysis

A SOC analyst may review:

- Windows Event Logs
- Linux system and authentication logs
- firewall logs
- DNS logs
- proxy and web logs
- email security events
- EDR telemetry
- cloud audit logs
- IDS or IPS alerts
- SIEM correlations

### 4.3 Context Collection

A suspicious event does not always prove that an attack occurred. Analysts therefore gather additional context, such as:

- the affected user’s role
- the importance and type of the device
- the origin and reputation of an IP address
- parent-child process relationships
- earlier related events
- known threat intelligence
- timing and frequency of the activity

### 4.4 Alert Classification

An investigation may result in classifications such as:

- **True Positive:** genuine malicious or unauthorised activity
- **Benign True Positive:** the rule correctly detected an event, but the activity was authorised
- **False Positive:** the alert incorrectly indicated a threat
- **False Negative:** malicious activity occurred without generating an alert

### 4.5 Escalation

An analyst should escalate when:

- the event is likely to be a real incident
- a critical system is involved
- multiple devices or users may be compromised
- a privileged account is affected
- data loss or exfiltration is suspected
- the case exceeds the analyst’s authority or expertise
- immediate containment may be required

  
### 4.6 Documentation

Good SOC documentation is concise, accurate, and verifiable. It records:

- the time of the event or alert
- affected systems and accounts
- relevant indicators
- investigative steps
- findings
- supporting evidence
- risk or severity classification
- actions taken or recommended

CISA describes the Cyber Defense Analyst role as analysing information collected from tools such as IDS alerts, firewalls, and network traffic logs in order to mitigate threats.

---

## 5. Tier 1, Tier 2, and Tier 3 Roles

Many SOCs use a tiered operating model. Exact titles and responsibilities vary, so the tier model should not be treated as a universal or mandatory standard.

### Tier 1 — Initial Alert Analyst

Tier 1 analysts are usually the first reviewers of incoming alerts.

Typical responsibilities include:

- receiving and prioritising alerts
- performing initial triage
- following established playbooks
- collecting basic evidence
- closing false positives
- escalating suspicious cases
- documenting tickets and findings

Important Tier 1 skills include:

- attention to detail
- accurate use of procedures
- clear documentation
- basic networking and operating-system knowledge
- timely escalation

### Tier 2 — Incident Investigator

Tier 2 analysts perform deeper investigations.

Typical responsibilities include:

- analysing escalated alerts
- correlating multiple data sources
- building attack timelines
- identifying affected systems and accounts
- assessing incident severity
- initiating containment
- applying threat intelligence and MITRE ATT&CK
- supporting Tier 1 analysts

### Tier 3 — Senior Analyst or Threat Hunter

Tier 3 work may include the most technically complex investigations.

Typical responsibilities include:

- investigating advanced incidents
- conducting proactive threat hunting
- supporting malware and forensic analysis
- developing new detections
- modelling attacker techniques
- identifying detection gaps
- proposing automation and process improvements
- mentoring other analysts

### Other SOC Roles

A mature SOC may also include:

- SOC Manager
- SOC Engineer
- Detection Engineer
- Incident Responder
- Threat Intelligence Analyst
- Threat Hunter
- Digital Forensics Analyst
- Malware Analyst
- Security Automation Engineer

---

## 6. NOC vs SOC

A **Network Operations Center** (NOC) and a **Security Operations Center** (SOC) may both perform continuous monitoring, but they focus on different outcomes.

| Aspect | NOC | SOC |
|---|---|---|
| Primary objective | Availability and performance | Security and threat management |
| Main question | Is the system operating correctly? | Is the system secure? |
| Typical event | Outage, latency, capacity issue | Suspicious login, malware, data theft |
| Main data | Performance and availability metrics | Security logs and alerts |
| Typical response | Troubleshooting and service restoration | Investigation, containment, and incident response |
| Key metrics | Uptime, latency, capacity | Detection and response time, incidents |

The teams often cooperate. A service outage may result from an ordinary technical fault, but it could also be caused by a cyberattack.

---

## 7. Typical Security Alert Lifecycle

A simplified alert lifecycle may be represented as follows:

```text
Data Source
    ↓
Detection Logic
    ↓
Alert
    ↓
Triage
    ↓
Context Collection and Investigation
    ↓
Classification
    ↓
Closure or Escalation
    ↓
Incident Response
    ↓
Lessons and Improvement
```

### 7.1 Data Generation

An endpoint, server, firewall, cloud platform, or other system records an event.

### 7.2 Detection

A security rule, analytical model, or product identifies a suspicious pattern.

### 7.3 Alert Creation

A SIEM, EDR, or another security platform generates an alert.

### 7.4 Triage

A Tier 1 analyst reviews the basic facts and priority.

### 7.5 Investigation

The analyst reviews additional logs, users, processes, network connections, and threat intelligence.

### 7.6 Decision

The event is closed, monitored further, or escalated.

### 7.7 Response

For a confirmed incident, the organisation limits damage, removes attacker access, and restores operations.

### 7.8 Improvement

The team considers whether:

- the detection performed correctly
- sufficient telemetry was available
- the rule should be tuned
- a new playbook or control is required
- lessons should be shared

---

## 8. Skills of an Effective SOC Analyst

### Technical Skills

- networking fundamental
- Windows and Linux knowledge
- log analysis
- SIEM operation
- endpoint security basics
- understanding of authentication
- basic scripting
- MITRE ATT&CK usage
- incident response fundamentals

### Non-Technical Skills

- analytical thinking
- accurate documentation
- clear communication
- time management
- prioritisation
- teamwork
- decision-making under pressure
- commitment to continuous learning

An effective analyst does more than operate tools. They ask relevant questions, look for relationships, test assumptions, and base decisions on evidence.

---

## 9. Example: Suspicious Login Alert

Assume the SIEM reports multiple failed logins followed by a successful login for the same user account.

The analyst may ask:

1. Which user account is affected?
2. Where did the login attempts originate?
3. Did all events originate from the same IP address?
4. Is the location and time normal for this user?
5. Was multi-factor authentication used?
6. Was the password recently changed?
7. Did unusual activity follow the login?
8. Is the affected account privileged?
9. Are other users showing similar activity?
10. Should the account be temporarily disabled or the case escalated?

This example shows why an alert alone is rarely enough. The analyst must collect and interpret context.

---

## 10. Chapter Summary

A SOC is a central part of an organisation’s security monitoring, analysis, and response capability. SOC analysts investigate events from different sources, classify alerts, escalate incidents, and document their findings.

The Tier 1, Tier 2, and Tier 3 model can help distribute responsibilities, but actual roles vary between organisations. An effective SOC depends not only on technology, but also on trained people, clear processes, cooperation, and continuous improvement.

---


## References

1. National Institute of Standards and Technology: **Security Operations Center — CSRC Glossary**  
   https://csrc.nist.gov/glossary/term/Security_Operations_Center

2. National Institute of Standards and Technology: **The NIST Cybersecurity Framework (CSF) 2.0**  
   https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20

3. National Institute of Standards and Technology: **SP 800-61 Rev. 3 — Incident Response Recommendations and Considerations for Cybersecurity Risk Management**  
   https://csrc.nist.gov/pubs/sp/800/61/r3/final

4. Cybersecurity and Infrastructure Security Agency: **Cyber Defense Analyst**  
   https://www.cisa.gov/careers/work-rolescyber-defense-analyst

5. MITRE ATT&CK: **Get Started with ATT&CK**  
   https://attack.mitre.org/resources/

---

[← Back to the English contents](../../README.md) | [Next chapter →](02-how-a-soc-works.md)
