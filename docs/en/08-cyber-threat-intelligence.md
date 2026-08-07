# 08 — Cyber Threat Intelligence

[← Back to the English contents](README.md) | [Magyar változat](../hu/08-cyber-threat-intelligence.md)

## Introduction

A SOC does not only monitor what happens inside its own systems. It is also useful to understand which attackers, methods, campaigns, and malicious infrastructure are active outside the organisation.

This is where **Cyber Threat Intelligence**, or CTI, can help.

The Hungarian National Cyber Security Center describes CTI as the analysis of data and information from different sources to identify threat trends, attack patterns, and potential risks.

This chapter introduces CTI in a beginner-friendly way.

## 1. Data, Information, and Intelligence

### Data

A single observation.

```text
203.0.113.45
```

### Information

The data has context.

```text
The IP address 203.0.113.45
was observed during malicious login attempts.
```

### Intelligence

The information has been analysed and turned into a conclusion that supports a decision.

```text
The address is associated with an active campaign
targeting VPN systems.
Our organisation uses a similar VPN product,
so related logs should be reviewed.
```

CTI is therefore more than collecting data.

## 2. Threat Actors

A **threat actor** is a person or group that may carry out cyber attacks.

Examples include:

- cybercriminal groups
- state-linked groups
- hacktivists
- insiders
- opportunistic attackers

Their goals may include financial gain, data theft, espionage, extortion, disruption, or political objectives.

## 3. Indicators of Compromise

**IoC** stands for *Indicator of Compromise*.

It is a technical clue associated with known or suspected malicious activity.

Examples include:

- IP addresses
- domains
- URLs
- file hashes
- email addresses
- file names

An IoC does not always prove malicious activity. Indicators may become outdated or lose their original context.

## 4. Hashes

A **hash** is a fixed-length value calculated from a file.

It can be compared to a digital fingerprint.

A common algorithm is SHA-256.

Hashes are useful for identifying a specific known file, but a small file change produces a completely different hash.

## 5. Tactics, Techniques, and Procedures

**TTP** stands for:

- Tactics
- Techniques
- Procedures

TTPs describe how an attacker behaves.

Example:

```text
A phishing email is sent.
The document starts PowerShell.
PowerShell downloads additional code.
A scheduled task is created.
```

MITRE ATT&CK provides a common language for describing adversary behaviour.

## 6. IoCs and TTPs

| IoC | TTP |
|---|---|
| specific clue | behaviour pattern |
| IP address | phishing |
| domain | PowerShell download |
| file hash | privilege escalation |
| may change quickly | often more persistent |

## 7. CTI Sources

### Internal Sources

Examples include:

- SIEM alerts
- firewall logs
- EDR data
- incident reports
- phishing reports
- malware analysis

### External Sources

Examples include:

- CERT and CSIRT advisories
- government cybersecurity alerts
- vendor reports
- open-source databases
- research blogs
- professional communities
- commercial CTI feeds

A **feed** is a continuously updated source of threat data.

## 8. Open-Source CTI

Examples include:

- MITRE ATT&CK
- MISP
- OpenCTI
- CISA publications
- CERT-EU reports
- Hungarian NCSC alerts

When using an open source, check who published it, when it was updated, what evidence supports it, and whether other trusted sources confirm it.

## 9. The Intelligence Cycle

A simplified CTI cycle is:

```text
1. Requirements
        ↓
2. Collection
        ↓
3. Processing
        ↓
4. Analysis
        ↓
5. Dissemination
        ↓
6. Feedback
        ↺
```

The process should begin with a clear question.

## 10. Strategic, Tactical, Operational, and Technical CTI

### Strategic

Supports higher-level decisions.

### Tactical

Focuses on attacker methods.

### Operational

Focuses on active campaigns.

### Technical

Provides concrete indicators such as domains and IP addresses.

Different sources may define these categories slightly differently.

## 11. Confidence

CTI reports often describe how confident the analyst is in a conclusion.

Examples include:

- low confidence
- medium confidence
- high confidence

CERT-EU's 2026 CTI Framework specifically addresses confidence and uncertainty.

## 12. Traffic Light Protocol

The **Traffic Light Protocol**, or TLP, indicates how information may be shared.

TLP 2.0 uses:

- TLP:RED
- TLP:AMBER
- TLP:GREEN
- TLP:CLEAR

In simple terms, RED is very restricted, AMBER is limited, GREEN is community sharing, and CLEAR allows unrestricted sharing.

## 13. STIX and TAXII

### STIX

STIX is a structured format for describing cyber threat intelligence.

It may describe indicators, malware, threat groups, relationships, and techniques.

### TAXII

TAXII is a mechanism for exchanging CTI between systems.

A simple comparison is:

```text
STIX = the format of the information
TAXII = the way it is transported
```

## 14. CTI in a SOC

Threat intelligence may support:

- alert enrichment
- threat hunting
- detection development
- prioritisation

Example hunting question:

```text
Did we communicate with this domain
during the last 30 days?
```

## 15. Simple CTI Example

A trusted CERT publishes:

```text
A new phishing campaign
targets financial organisations.

Related domain:
secure-login-example.com

Method:
fake Microsoft 365 login page
```

The SOC may:

1. search DNS logs for the domain
2. search email logs for the link
3. check whether users clicked it
4. block the domain when appropriate
5. notify affected users
6. create a new detection rule

External information has now become a defensive action.

## 16. Limitations of CTI

Possible problems include:

- outdated indicators
- unreliable sources
- incorrect attribution
- missing context
- too many low-value indicators
- information that is irrelevant to your organisation

Good CTI should be relevant, timely, reliable, understandable, and actionable.

## 17. Key Points for Beginners

- CTI is analysed information, not just collected data.
- An IoC is a specific technical clue.
- A TTP describes attacker behaviour.
- MITRE ATT&CK provides a common language for adversary behaviour.
- CTI can come from internal and external sources.
- Not every feed is relevant to every organisation.
- Confidence and uncertainty should be communicated.
- TLP describes information-sharing boundaries.
- STIX structures CTI data and TAXII can transport it.
- CTI is most useful when it supports a concrete defensive decision.

## 18. Review Questions

1. What does CTI stand for?
2. How do data, information, and intelligence differ?
3. What is a threat actor?
4. What is an IoC?
5. What is a hash?
6. What does TTP mean?
7. How do IoCs and TTPs differ?
8. Which internal CTI sources may exist?
9. Which external sources may be used?
10. What are the main steps of the intelligence cycle?
11. What is strategic CTI?
12. What does confidence mean?
13. What is TLP used for?
14. How do STIX and TAXII differ?
15. How can a SOC use CTI?

## References

1. Hungarian National Cyber Security Center  
   **Kiberfenyegetettség elemzés** [Hungarian]  
   https://nki.gov.hu/intezet/tartalom/magunkrol/

2. Hungarian National Cyber Security Center  
   **Egy ingyenes nyílt forrású CTI platform** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/tanacsok/egy-ingyenes-nyilt-forrasu-cti-cyber-threat-intelligence-platform/

3. National University of Public Service  
   **Kiberfenyegetettség elemzés – képzési program** [Hungarian]  
   https://kti.uni-nke.hu/document/vtkk-uni-nke-hu/Elektronikus%20inform%C3%A1ci%C3%B3biztons%C3%A1gi%20vezet%C5%91%20-%20K%C3%A9pz%C3%A9si%20program%202025.pdf

4. MITRE ATT&CK  
   **Get Started – Threat Intelligence**  
   https://attack.mitre.org/resources/get-started/threat-intelligence/

5. MITRE ATT&CK  
   **CTI Training**  
   https://attack.mitre.org/resources/training/cti/

6. CERT-EU  
   **Cyber Threat Intelligence Framework**  
   https://www.cert.europa.eu/publications/threat-intelligence/cyber-threat-intelligence-framework/

7. CISA  
   **Information Sharing**  
   https://www.cisa.gov/topic/cybersecurity-information-sharing

8. FIRST  
   **Traffic Light Protocol 2.0**  
   https://www.first.org/tlp/

9. MITRE ATT&CK  
   **ATT&CK Data and Tools – STIX**  
   https://attack.mitre.org/resources/attack-data-and-tools/

---

[← Previous chapter](07-siem-fundamentals.md) | [Back to contents](README.md) | [Next chapter →](09-mitre-attack.md)
