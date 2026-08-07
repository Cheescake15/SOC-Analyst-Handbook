# 09 — MITRE ATT&CK

[← Back to the English contents](README.md) | [Magyar változat](../hu/09-mitre-attack.md)

## Introduction

The previous chapter introduced TTPs, meaning the tactics, techniques, and procedures used by attackers.

MITRE ATT&CK is a public knowledge base that organises these adversary behaviours.

ATT&CK stands for *Adversarial Tactics, Techniques, and Common Knowledge*.

In simple terms, MITRE ATT&CK provides a common language for describing how attackers behave during cyber operations.

## 1. Why Was ATT&CK Created?

MITRE developed ATT&CK to document and organise behaviours observed in real-world attacks.

The knowledge base does not provide instructions for carrying out an attack. It describes the goals attackers pursue and the behaviours that defenders have observed.

MITRE describes ATT&CK as a knowledge base of adversary techniques based on real-world observations.

## 2. Tactics, Techniques, Sub-Techniques, and Procedures

### Tactic

A tactic describes **why** an attacker performs an action.

Example:

```text
Initial Access
```

The attacker's goal is to gain access to the target environment.

Another example:

```text
Credential Access
```

The attacker wants to obtain credentials.

### Technique

A technique describes **how** the attacker attempts to achieve a tactical goal.

For example, a possible Initial Access technique is phishing.

### Sub-Technique

A sub-technique provides a more specific description of a technique.

Phishing may involve a malicious attachment, malicious link, or another specific method.

### Procedure

A procedure describes how a particular attacker or group implemented a technique in a real operation.

A simple summary:

```text
Tactic = Why?
Technique = How?
Sub-technique = More specifically how?
Procedure = How did a real attacker do it?
```

## 3. The ATT&CK Matrix

The ATT&CK Matrix is the best-known visual part of ATT&CK.

Its columns represent tactical goals, while the entries underneath them represent techniques.

The matrix may look complex at first. Beginners do not need to memorise it.

It is better to think of it as a map that helps organise observed attacker behaviour.

## 4. ATT&CK Technology Domains

Important ATT&CK domains include:

- Enterprise
- Mobile
- ICS

### Enterprise

Covers traditional enterprise environments and cloud technologies.

This is usually the most relevant domain for a SOC analyst.

### Mobile

Covers adversary behaviour involving mobile devices.

### ICS

Covers industrial control systems.

ATT&CK changes over time, so the current online version should always be checked.

## 5. Some Important Enterprise Tactics

The full list does not need to be memorised.

### Reconnaissance

The attacker gathers information about the target.

### Initial Access

The attacker attempts to enter the environment.

Examples include phishing, exploiting public-facing systems, and using valid accounts.

### Execution

The attacker runs code or commands.

### Persistence

The attacker tries to maintain access.

Examples include scheduled tasks and new accounts.

### Privilege Escalation

The attacker attempts to gain higher privileges.

### Credential Access

The attacker tries to obtain passwords or other authentication data.

### Discovery

The attacker learns more about the environment.

### Lateral Movement

The attacker moves from one system to another.

### Collection

The attacker gathers data of interest.

### Command and Control

A compromised device communicates with attacker-controlled infrastructure.

This is often shortened to C2 or C&C.

### Exfiltration

The attacker transfers data out of the organisation.

### Impact

The attacker attempts to disrupt or damage systems and data.

## 6. ATT&CK Is Not a Straight Timeline

The Matrix should not be treated as a mandatory sequence.

An attacker may:

- skip tactics
- return to earlier activities
- pursue several goals at once
- use one technique for several purposes

ATT&CK is therefore not simply a flowchart.

## 7. Technique IDs

ATT&CK techniques have identifiers.

Example:

```text
T1059
```

This identifies Command and Scripting Interpreter.

A sub-technique may look like:

```text
T1059.001
```

This refers to PowerShell.

Identifiers are useful because they provide an unambiguous way to reference techniques across tools and languages.

## 8. Simple ATT&CK Example

Suppose an investigation shows:

```text
1. A user receives a malicious email.
2. The user opens a link.
3. A program starts PowerShell.
4. A scheduled task is created.
5. The device connects to an external server.
```

A simplified mapping could be:

| Observation | Possible ATT&CK category |
|---|---|
| malicious email | Initial Access |
| PowerShell | Execution |
| scheduled task | Persistence |
| external control server | Command and Control |

This is not a complete analysis, but it helps organise the events.

## 9. ATT&CK and Cyber Threat Intelligence

CTI reports often use ATT&CK techniques to describe a threat group's behaviour.

For example, a report may describe a group as frequently using:

- phishing
- PowerShell
- credential theft
- remote services
- scheduled tasks

These behaviours can be mapped to ATT&CK.

This makes different reports easier to compare.

## 10. ATT&CK in a SOC

A SOC may use ATT&CK for:

### Alert Tagging

A SIEM alert can be tagged with a related ATT&CK technique.

### Finding Detection Gaps

The SOC can review which important techniques have detections and which do not.

### Threat Hunting

Known techniques used by a relevant threat group may guide targeted searches.

### Incident Documentation

Incident activity can be described using consistent ATT&CK terminology.

### CTI Processing

Behaviours described in external reports can be mapped to ATT&CK techniques.

## 11. Detection Coverage

**Detection coverage** describes which ATT&CK techniques an organisation has some ability to detect.

Example:

```text
Phishing → email detection exists
PowerShell → logging and detection exist
Scheduled Task → partial detection
Credential Dumping → insufficient data source
```

A technique marked as covered does not mean every possible form of that technique will be detected.

MITRE specifically warns against treating ATT&CK as a simple checklist.

## 12. ATT&CK Navigator

The **ATT&CK Navigator** is a web-based tool for visually working with ATT&CK matrices.

Techniques can be:

- selected
- coloured
- scored
- annotated
- organised in layers

A SOC might create one layer showing its detection coverage and another showing the techniques used by a relevant threat group.

Comparing the two may help identify priorities.

## 13. Groups and Software

ATT&CK also contains information about:

- known threat groups
- malware
- adversary tools
- campaigns

A group page may show techniques that public reporting has associated with that group.

This information should not be treated as complete or absolute. ATT&CK is based on documented observations.

## 14. What Is Mapping?

**Mapping** means connecting an observed behaviour to an ATT&CK technique.

Example:

```text
The attacker executed PowerShell.
```

This may be mapped to the PowerShell sub-technique.

Good mapping requires understanding:

- what the attacker did
- the purpose of the activity
- how it was performed
- whether enough evidence exists

## 15. A Common Beginner Mistake

It is easy to map too quickly.

Example:

```text
powershell.exe started
```

This only proves that PowerShell ran.

It does not yet tell us:

- who launched it
- which command was used
- whether it was normal administration
- whether it was connected to an attack

ATT&CK mapping does not replace investigation.

## 16. Limitations of ATT&CK

### It Does Not Contain Every Possible Behaviour

ATT&CK can only document observed and reported behaviours.

The Hungarian National Cyber Security Center has reported malware using a Linux persistence method that was not yet included in ATT&CK at the time.

### It Changes Over Time

Techniques and structures may be added or modified.

### It Is Not a Risk Score

ATT&CK does not automatically tell an organisation how dangerous a technique is for its own environment.

### It Is Not a Checklist

The goal is not to colour every box green.

Relevant threats should be prioritised.

## 17. Key Points for Beginners

- MITRE ATT&CK organises real-world adversary behaviour.
- A tactic describes the attacker's goal.
- A technique describes how the goal may be achieved.
- A sub-technique provides a more specific description.
- Techniques have unique IDs.
- The Matrix is not a mandatory attack sequence.
- ATT&CK supports CTI, detection, and threat hunting.
- ATT&CK Navigator helps visualise techniques.
- Detection coverage does not automatically mean complete protection.
- ATT&CK does not replace analyst judgement.

## 18. Review Questions

1. What is MITRE ATT&CK?
2. What does ATT&CK stand for?
3. What is a tactic?
4. What is a technique?
5. What is a sub-technique?
6. What is a procedure?
7. What is the ATT&CK Matrix used for?
8. Which major technology domains exist?
9. What does Initial Access mean?
10. What does Persistence mean?
11. What does Lateral Movement mean?
12. Why are technique IDs useful?
13. How can a SOC use ATT&CK?
14. What is ATT&CK Navigator used for?
15. Why should ATT&CK not be treated as a simple checklist?

## References

1. MITRE ATT&CK  
   **Get Started**  
   https://attack.mitre.org/resources/

2. MITRE ATT&CK  
   **Enterprise Tactics**  
   https://attack.mitre.org/tactics/

3. MITRE ATT&CK  
   **Frequently Asked Questions**  
   https://attack.mitre.org/resources/faq/

4. MITRE ATT&CK  
   **ATT&CK Data & Tools**  
   https://attack.mitre.org/resources/attack-data-and-tools/

5. MITRE ATT&CK  
   **CTI Training**  
   https://attack.mitre.org/resources/training/cti/

6. Hungarian National Cyber Security Center  
   **Éves kiberbiztonsági jelentés** [Hungarian]  
   https://nki.gov.hu/wp-content/uploads/2024/07/Eves-kiberbiztonsagi-jelentes.pdf

7. Hungarian National Cyber Security Center  
   **Androidos felhasználók után kémkedett egy applikáció** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/hirek/androidos-felhasznalok-utan-kemkedett-egy-applikacio/

8. Hungarian National Cyber Security Center  
   **A sedexp Linux malware éveken át észrevétlen maradt** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/hirek/a-sedexp-linux-malware-eveken-at-eszrevetlen-maradt/

---

[← Previous chapter](08-cyber-threat-intelligence.md) | [Back to contents](README.md) | [Next chapter →](10-incident-response.md)
