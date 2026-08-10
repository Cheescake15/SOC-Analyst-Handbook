# 15 — References

[← Back to the English contents](README.md) | [Magyar változat](../hu/15-references.md)

## Introduction

The SOC Analyst Handbook is primarily based on official, verifiable, and professionally trusted sources.

The goal was not to collect as many links as possible.

Sources were selected because they are:

- useful for beginners
- professionally credible
- regularly maintained
- suitable for further learning
- connected to real defensive practice

The references are organised by topic.

## 1. NIST

The National Institute of Standards and Technology, or NIST, is one of the most important cybersecurity reference organisations.

### NIST Cybersecurity Framework 2.0

https://www.nist.gov/cyberframework

The framework helps organisations manage cybersecurity risk.

Its main functions are:

- Govern
- Identify
- Protect
- Detect
- Respond
- Recover

### NIST SP 800-61 Rev. 3

Incident Response Recommendations and Considerations for Cybersecurity Risk Management

https://csrc.nist.gov/pubs/sp/800/61/r3/final

This publication was an important source for the Incident Response chapter.

### NIST Incident Response Project

https://csrc.nist.gov/projects/incident-response

Contains additional incident response material.

## 2. CISA

The Cybersecurity and Infrastructure Security Agency, or CISA, publishes practical cybersecurity guidance and advisories.

### Use Logging on Business Systems

https://www.cisa.gov/audiences/small-and-medium-businesses/secure-your-business/use-logging-on-business-systems

Useful beginner guidance on why security logging matters.

### Cybersecurity Incident and Vulnerability Response Playbooks

https://www.cisa.gov/sites/default/files/2024-08/Federal_Government_Cybersecurity_Incident_and_Vulnerability_Response_Playbooks_508C.pdf

Provides structured incident and vulnerability response processes.

### Cybersecurity Information Sharing

https://www.cisa.gov/topic/cybersecurity-information-sharing

Background material on sharing threat information.

## 3. MITRE ATT&CK

MITRE ATT&CK is one of the most important public knowledge bases for adversary behaviour.

Main site:

https://attack.mitre.org/

### Get Started

https://attack.mitre.org/resources/

A useful starting point for beginners.

### Enterprise Tactics

https://attack.mitre.org/tactics/

Lists ATT&CK Enterprise tactics.

### Data Sources

https://attack.mitre.org/datasources/

Describes data sources relevant to detecting attacker behaviour.

### CTI Training

https://attack.mitre.org/resources/training/cti/

Training material connecting CTI and ATT&CK.

### ATT&CK Data and Tools

https://attack.mitre.org/resources/attack-data-and-tools/

Resources for ATT&CK data and tooling.

### Adversary Emulation Plans

https://attack.mitre.org/resources/adversary-emulation-plans/

Structured material for modelling adversary behaviour.

## 4. Microsoft Learn

Microsoft Learn was an important source for Windows, PowerShell, Microsoft Sentinel, and incident investigation topics.

Main site:

https://learn.microsoft.com/

### Windows Security Events

Example:

https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/event-4624

Used for interpreting Windows security events.

### Windows Event Log

https://learn.microsoft.com/en-us/windows/win32/wes/windows-event-log

Technical documentation for Windows logging.

### PowerShell Logging

https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging

Describes PowerShell logging capabilities.

### Microsoft Sentinel

https://learn.microsoft.com/en-us/azure/sentinel/

A major source for the SIEM, detection, incident, and triage chapters.

### Scheduled Analytics Rules

https://learn.microsoft.com/en-us/azure/sentinel/scheduled-rules-overview

Detailed background on SIEM analytics rules.

### Incident Investigation

https://learn.microsoft.com/en-us/azure/sentinel/investigate-incidents

Explains incident investigation, alerts, evidence, and entities.

## 5. Ubuntu Documentation

Official Ubuntu documentation was used for the Linux chapter.

### User Management

https://ubuntu.com/server/docs/how-to/security/user-management/

### OpenSSH Server

https://ubuntu.com/server/docs/how-to/security/openssh-server/

### Security Suggestions

https://ubuntu.com/server/docs/explanation/security/security_suggestions/

These resources provide practical background on accounts, SSH, and Linux security.

## 6. IETF

The Internet Engineering Task Force, or IETF, publishes core internet standards.

The Network Fundamentals chapter used several RFC documents.

### TCP — RFC 9293

https://datatracker.ietf.org/doc/html/rfc9293

### IPv6 — RFC 8200

https://datatracker.ietf.org/doc/html/rfc8200

### DNS — RFC 1034

https://datatracker.ietf.org/doc/html/rfc1034

### DNS — RFC 1035

https://datatracker.ietf.org/doc/html/rfc1035

### HTTP Semantics — RFC 9110

https://datatracker.ietf.org/doc/html/rfc9110

These are technical standards.

Beginners do not need to read them completely.

They are especially useful for checking definitions and protocol behaviour.

## 7. Sigma Detection Format

Sigma is an open and vendor-neutral detection rule format.

Main site:

https://sigmahq.io/

### Documentation

https://sigmahq.io/docs/

### Sigma Rules

https://sigmahq.io/docs/basics/rules.html

The Detection Engineering chapter uses Sigma to demonstrate how detection logic can be written in a structured and portable way.

## 8. FIRST and TLP

The Forum of Incident Response and Security Teams, or FIRST, maintains several international security collaboration resources.

### Traffic Light Protocol 2.0

https://www.first.org/tlp/

TLP defines information-sharing boundaries.

The labels used in the handbook are:

- TLP:RED
- TLP:AMBER
- TLP:GREEN
- TLP:CLEAR

## 9. CERT-EU

CERT-EU supports the cybersecurity community of European Union institutions and bodies.

### Cyber Threat Intelligence Framework

https://www.cert.europa.eu/publications/threat-intelligence/cyber-threat-intelligence-framework/

Used as a source for the CTI lifecycle, analytical confidence, and uncertainty.


## 10. National University of Public Service

An important Hungarian-language academic source was:

### Az információbiztonság alapjai

Edited by Gyaraki Réka

National University of Public Service, 2023

https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

The book provides broad background on:

- information security concepts
- risk management
- organisational security
- network and system security

It was used as a supporting source in several chapters.

## 11. MISP

MISP, or Malware Information Sharing Platform, is an open-source threat intelligence platform.

https://www.misp-project.org/

It supports:

- IoC storage
- threat information sharing
- relationship management
- structured intelligence exchange

It can be a useful next topic after the beginner CTI chapter.

## 12. OpenCTI

OpenCTI is an open-source Cyber Threat Intelligence platform.

https://filigran.io/solutions/opencti/

It can support:

- organising threat actors
- managing IoCs
- linking ATT&CK techniques
- visualising CTI relationships

The Hungarian National Cyber Security Center has also published an introduction to OpenCTI.

## 13. Additional Learning Resources

Practical learning environments can complement official documentation.

Examples include:

- Microsoft Learn
- CyberDefenders
- Blue Team Labs Online
- TryHackMe blue-team material
- LetsDefend
- MITRE ATT&CK training

These should always be used in authorised training environments.

## 14. How to Evaluate a Source

Useful questions include:

1. Who published it?
2. Is it an official organisation or recognised professional source?
3. When was it updated?
4. Does it cite primary sources?
5. Do other trusted sources confirm it?
6. Does it separate facts from opinion?
7. Does it communicate uncertainty?

## 15. Primary and Secondary Sources

### Primary Source

The original document or data.

Examples:

- NIST publication
- Microsoft documentation
- MITRE ATT&CK technique page
- IETF RFC
- CISA advisory

### Secondary Source

Explains or summarises a primary source.

Examples include:

- professional blogs
- textbooks
- educational articles
- news coverage

Where possible, this handbook uses primary sources and supplements them with Hungarian-language professional material.

## 16. Why Freshness Matters

Cybersecurity changes quickly.

The following may change:

- product features
- Windows event documentation
- ATT&CK techniques
- SIEM capabilities
- vulnerability status
- active threat campaigns

The current version of an original source should therefore be checked when using the handbook.

## 17. Role of Research in This Project

The goal was to create more than a collection of personal notes.

Research makes it possible to:

- verify definitions
- trace professional claims
- provide further learning paths
- improve the credibility of the repository
- update the project more easily later

## 18. Suggested Learning Path

A possible next learning sequence is:

```text
1. NIST CSF
2. Windows and Linux logging
3. Microsoft Sentinel or another SIEM
4. MITRE ATT&CK
5. Sigma
6. CTI
7. Incident Response
8. Practical blue-team labs
```

There is no need to learn everything at once.

## 19. Final Note

No cybersecurity handbook remains permanently complete.

New technologies, attacker methods, and defensive tools continue to appear.

For this reason, I see this repository as a learning project that can continue to grow.

The goal was not to create an expert-level encyclopedia.

The goal was to create a beginner-friendly handbook that:

- organises the fundamentals
- supports further learning
- points to trustworthy sources
- can later be extended with new chapters and practical examples

---

[← Previous chapter](14-cheat-sheet.md) | [Back to contents](README.md)
