# 08 — Cyber Threat Intelligence

[← Back to the English contents](README.md) | [Magyar változat](../hu/08-cyber-threat-intelligence.md)

## Introduction

A SOC does not only monitor what happens inside its own systems. It is also useful to understand which attackers, methods, campaigns, and malicious infrastructure are active outside the organisation.

This is where **Cyber Threat Intelligence**, or CTI, can help.

CTI turns collected data into analysed information that can support security decisions.

This chapter introduces the most important CTI concepts in a beginner-friendly way.

## 1. Data, Information, and Intelligence

### Data

A single observation.

```text
203.0.113.45
```

This is only an IP address.

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
Our organisation uses a similar product,
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

- IP address
- domain
- URL
- file hash
- email address
- file name

An IoC does not always prove malicious activity. Context and timing matter.

## 4. Hashes

A **hash** is a value calculated from a file.

It can be compared to a digital fingerprint.

A common algorithm is SHA-256.

Hashes are useful for finding a specific known file. A small change to a file produces a different hash.

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
| domain | PowerShell use |
| file hash | privilege escalation |
| may change quickly | often more persistent |

An attacker can replace an IP address quickly. Changing established methods may take more effort.

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
- government alerts
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

When using an open source, check:

- who published it
- when it was updated
- what evidence supports it
- whether trusted sources confirm it

## 9. The Intelligence Cycle

A simplified cycle is:

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

The process starts with a clear question.

## 10. Strategic, Tactical, Operational, and Technical CTI

### Strategic

Supports higher-level decisions.

### Tactical

Focuses on attacker methods.

### Operational

Focuses on active campaigns.

### Technical

Provides concrete indicators such as domains, IP addresses, and hashes.

Different sources may define these categories slightly differently.

## 11. Confidence

CTI reports often describe how confident the analyst is in a conclusion.

Examples:

- low confidence
- medium confidence
- high confidence

Observed facts should be separated from analytical judgement.

## 12. Traffic Light Protocol

The **Traffic Light Protocol**, or TLP, indicates how information may be shared.

TLP 2.0 uses:

- TLP:RED
- TLP:AMBER
- TLP:GREEN
- TLP:CLEAR

In simple terms:

- RED means very restricted sharing
- AMBER means limited sharing
- GREEN allows sharing within a community
- CLEAR allows unrestricted sharing

## 13. STIX and TAXII

### STIX

STIX is a structured format for describing cyber threat intelligence.

### TAXII

TAXII supports the exchange of CTI between systems.

A simple comparison:

```text
STIX = the format
TAXII = the transport
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
- information that is irrelevant to the organisation

Good CTI should be:

- relevant
- timely
- reliable
- understandable
- actionable

## 17. Key Points for Beginners

- CTI is analysed information, not just collected data.
- An IoC is a specific technical clue.
- A TTP describes attacker behaviour.
- MITRE ATT&CK helps organise adversary techniques.
- CTI can come from internal and external sources.
- Sources should be checked for reliability.
- Confidence communicates uncertainty.
- TLP describes information-sharing boundaries.
- STIX is a format and TAXII supports transport.
- CTI is most useful when it supports a concrete decision.

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

3. MITRE ATT&CK  
   **Get Started – Threat Intelligence**  
   https://attack.mitre.org/resources/get-started/threat-intelligence/

4. MITRE ATT&CK  
   **CTI Training**  
   https://attack.mitre.org/resources/training/cti/

5. CERT-EU  
   **Cyber Threat Intelligence Framework**  
   https://www.cert.europa.eu/publications/threat-intelligence/cyber-threat-intelligence-framework/

6. CISA  
   **Information Sharing**  
   https://www.cisa.gov/topic/cybersecurity-information-sharing

7. FIRST  
   **Traffic Light Protocol 2.0**  
   https://www.first.org/tlp/

8. MITRE ATT&CK  
   **ATT&CK Data and Tools – STIX**  
   https://attack.mitre.org/resources/attack-data-and-tools/

---

[← Previous chapter](07-siem-fundamentals.md) | [Back to contents](README.md) | [Next chapter →](09-mitre-attack.md)
