# 10 — Incident Response

[← Back to the English contents](README.md) | [Magyar változat](../hu/10-incident-response.md)

## Introduction

A security alert does not automatically mean that a real attack occurred. When an investigation confirms a cybersecurity problem, the organisation needs to respond.

This process is called incident response.

Its goals include:

- identifying the problem quickly
- limiting damage
- removing the attacker's presence
- restoring operations safely
- understanding what happened
- learning from the incident

NIST SP 800-61 Rev. 3 treats incident response as part of broader cybersecurity risk management.

## 1. Security Event and Incident

A security event is something that may be relevant from a security perspective.

```text
A user entered the wrong password three times.
```

This is not automatically an incident.

A **cybersecurity incident** is an event or sequence of events that may actually harm systems or data.

Examples include unauthorised access, malware, data theft, ransomware, privilege abuse, and service disruption.

## 2. Preparation

Good incident response begins before an incident occurs.

An organisation should know:

- who is responsible
- who must be notified
- which logs are collected
- how escalation works
- who may isolate a system
- which communication channels are available
- where backups are stored
- when external support is needed

## 3. Incident Response Plan

An **incident response plan** defines responsibilities and important processes in advance.

It may include:

- roles
- contacts
- incident categories
- escalation rules
- communication procedures
- documentation requirements
- external reporting procedures

## 4. Playbooks

A **playbook** is a more specific guide for one type of incident.

Examples include:

- phishing
- ransomware
- compromised account
- malware infection

A phishing playbook may ask whether a user clicked a link, entered a password, or whether other users received the same message.

## 5. Detection and Analysis

Alerts may come from:

- SIEM
- EDR
- antivirus
- firewall
- user reports
- external CERT or CSIRT notifications

The analyst may review users, IP addresses, processes, files, network connections, and related alerts.

## 6. Triage

**Triage** is a quick first assessment.

It helps answer:

- Is this probably real?
- How urgent is it?
- Which system is affected?
- How many users are involved?
- Does it require escalation?

## 7. Containment

**Containment** means limiting the incident so that it cannot spread or cause more damage.

Possible actions include:

- isolating a device
- disabling a compromised account
- blocking a malicious domain
- blocking an attacker IP
- restricting an affected service

A critical system should not be shut down without considering the business impact.

## 8. Eradication

**Eradication** means removing the attacker's presence and the cause of the problem.

Examples include:

- removing malware
- deleting a malicious account
- fixing a vulnerability
- changing compromised credentials
- removing a malicious scheduled task

## 9. Recovery

**Recovery** means restoring normal operations safely.

Possible actions include:

- reinstalling systems
- restoring backups
- changing passwords
- applying updates
- restarting services
- increasing monitoring

The goal is safe recovery, not only fast recovery.

## 10. Preserving Evidence

Useful evidence may include:

- logs
- emails
- files
- memory data
- disk images
- network data
- screenshots
- timelines

Important facts should be documented, including when and where evidence was collected.

## 11. Chain of Custody

**Chain of custody** records how evidence was handled.

```text
09:20 — disk image created
09:25 — SHA-256 hash recorded
09:30 — evidence stored securely
09:35 — handed to forensic analyst
```

This may be especially important in legal or regulatory cases.

## 12. Documentation

A timeline may look like:

```text
10:12 — alert received
10:17 — user contacted
10:25 — unauthorised access confirmed
10:31 — account disabled
10:45 — device isolated
```

Documentation supports investigations, handovers, and later review.

## 13. Communication

Serious incidents may involve:

- SOC
- IT
- management
- legal teams
- privacy specialists
- communications staff
- HR
- external providers

Organisations should know in advance who may communicate internally and externally.

## 14. Lessons Learned

After an incident, useful questions include:

- How did the attacker gain access?
- What worked well?
- What slowed the investigation?
- Which logs were missing?
- Do we need a new detection rule?
- Should the playbook change?
- Is training required?

The goal is improvement, not blame.

## 15. NIST's Current Approach

A traditional model often describes:

```text
Preparation
Detection and Analysis
Containment, Eradication and Recovery
Post-Incident Activity
```

NIST SP 800-61 Rev. 3 aligns incident response with Cybersecurity Framework 2.0:

```text
Govern
Identify
Protect
Detect
Respond
Recover
```

This emphasises that effective response depends on work done before an alert appears.

## 16. Simple Ransomware Example

```text
09:05 — user reports inaccessible files
09:08 — SOC checks EDR alert
09:12 — device isolated
09:17 — similar activity searched on other devices
09:25 — another affected device identified
09:30 — incident escalated
```

Real ransomware incidents may be much more complex.

## 17. What Should a Beginner Avoid?

Without approval, a beginner should not:

- shut down many systems
- delete files
- modify evidence
- actively connect to attacker infrastructure
- communicate publicly
- run unknown tools on production systems

Knowing when to escalate is an important SOC skill.

## 18. Key Points for Beginners

- Not every security event is an incident.
- Preparation starts before the incident.
- Triage helps determine urgency.
- Containment limits spread.
- Eradication removes the cause and attacker presence.
- Recovery restores operations safely.
- Evidence should be handled carefully.
- Important actions should be documented.
- Incident response is both technical and organisational.
- Lessons learned improve future response.
- When unsure, escalate.

## 19. Review Questions

1. How do an event and an incident differ?
2. What is the goal of incident response?
3. Why is preparation important?
4. What is an incident response plan?
5. What is a playbook?
6. What does triage mean?
7. What is containment?
8. What is eradication?
9. What is recovery?
10. Why should evidence be preserved?
11. What is chain of custody?
12. Why is documentation important?
13. What are lessons learned?
14. Why do several organisational teams need to cooperate?
15. What does NIST SP 800-61 Rev. 3 emphasise?

## References

1. National Institute of Standards and Technology  
   **NIST SP 800-61 Rev. 3 — Incident Response Recommendations and Considerations for Cybersecurity Risk Management**  
   https://csrc.nist.gov/pubs/sp/800/61/r3/final

2. National Institute of Standards and Technology  
   **Incident Response Project**  
   https://csrc.nist.gov/projects/incident-response

3. Cybersecurity and Infrastructure Security Agency  
   **Federal Government Cybersecurity Incident and Vulnerability Response Playbooks**  
   https://www.cisa.gov/sites/default/files/2024-08/Federal_Government_Cybersecurity_Incident_and_Vulnerability_Response_Playbooks_508C.pdf

4. Hungarian National Cyber Security Center  
   **Incidenskezelés** [Hungarian]  
   https://nki.gov.hu/szolgaltatasok/tartalom/incidenskezeles/

5. Hungarian National Cyber Security Center  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

6. Gyaraki Réka, editor  
   **Az információbiztonság alapjai** [Hungarian]  
   National University of Public Service, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Previous chapter](09-mitre-attack.md) | [Back to contents](README.md) | [Next chapter →](11-malware-basics.md)
