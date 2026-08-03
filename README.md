# SOC Analyst Handbook
[English](README.md) | [Magyar](README.hu.md)

> A practical, beginner-friendly guide to Security Operations Center workflows, log analysis, threat detection, incident response, and hands-on blue team skills.

## Overview

The **SOC Analyst Handbook** is an educational and portfolio-oriented project for students and aspiring blue team professionals. It combines concise theoretical explanations with practical examples, detection content, investigation workflows, and guided labs.

The handbook is designed to help readers:

- understand how a modern Security Operations Center operates;
- build essential networking, Windows, Linux, and log-analysis knowledge;
- become familiar with SIEM, EDR, threat intelligence, and detection engineering;
- map suspicious activity to MITRE ATT&CK;
- follow a structured incident-response process;
- practise common Tier 1 and junior Tier 2 analyst tasks in safe lab environments.

## Intended Audience

This repository is intended for:

- cybersecurity students;
- aspiring SOC analysts;
- junior blue team professionals;
- IT professionals transitioning into cybersecurity;
- anyone preparing for an entry-level security operations role.

No advanced programming knowledge is required. Basic IT and networking knowledge is helpful.

## Learning Objectives

After working through the handbook, readers should be able to:

1. explain the purpose and structure of a SOC;
2. describe common Tier 1, Tier 2, and Tier 3 responsibilities;
3. interpret basic network traffic and common protocols;
4. identify relevant Windows and Linux security events;
5. analyse logs and recognise suspicious patterns;
6. write basic SIEM queries in SPL and KQL;
7. understand Sigma and YARA rule structure;
8. distinguish indicators of compromise from attacker behaviours;
9. use MITRE ATT&CK to classify observed activity;
10. document and escalate a security incident clearly.

## Repository Structure

```text
soc-analyst-handbook/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── SECURITY.md
├── .gitignore
├── docs/
├── diagrams/
├── images/
├── labs/
├── scripts/
└── detections/
    ├── sigma/
    ├── yara/
    ├── kql/
    └── spl/
```

## Handbook Chapters

| No. | Chapter | Main topics |
|---:|---|---|
| 01 | Introduction to Security Operations | SOC purpose, blue team, analyst roles, NOC vs SOC |
| 02 | How a SOC Works | People, processes, technology, alert lifecycle, escalation |
| 03 | Network Fundamentals | OSI, TCP/IP, DNS, HTTP(S), DHCP, ARP, ICMP |
| 04 | Windows Security | Event Viewer, authentication, processes, services, registry, PowerShell |
| 05 | Linux Security | Users, permissions, sudo, authentication logs, systemd, cron |
| 06 | Log Analysis | Event logs, Sysmon, web server, firewall and authentication logs |
| 07 | SIEM Fundamentals | Splunk, Microsoft Sentinel, Wazuh, QRadar, searches and dashboards |
| 08 | Cyber Threat Intelligence | IOC, IOA, TTP, CVE, CVSS, STIX, TAXII |
| 09 | MITRE ATT&CK | Tactics, techniques, mapping and investigation support |
| 10 | Incident Response | Preparation, detection, response, recovery and improvement |
| 11 | Malware Basics | Trojans, worms, RATs, rootkits, ransomware and spyware |
| 12 | Detection Engineering | Sigma, YARA, KQL, SPL and detection lifecycle |
| 13 | Hands-on Labs | Wireshark, Windows logs, Sysmon, Splunk and Wazuh |
| 14 | SOC Analyst Cheat Sheet | Commands, event IDs, ports, queries and investigation prompts |
| 15 | References | Standards, official documentation and further reading |

## Hands-on Content

The repository will include guided exercises such as:

- analysing a TCP three-way handshake in Wireshark;
- investigating repeated failed Windows logons;
- identifying suspicious PowerShell activity;
- reviewing Sysmon process-creation events;
- writing a basic Sigma detection rule;
- creating elementary SPL and KQL searches;
- mapping an observed attack chain to MITRE ATT&CK;
- preparing a short SOC incident report.

All exercises must be performed only in systems that the learner owns or is explicitly authorised to test.

## Example Detection Content

The `detections/` directory contains educational examples for:

- **Sigma** — platform-independent log detection rules;
- **YARA** — file and malware pattern matching;
- **KQL** — Microsoft Sentinel and Defender hunting queries;
- **SPL** — Splunk searches.

Detection examples are learning materials and should be tested, tuned, and validated before any production use.

## Suggested Lab Environment

A safe learning environment may include:

- a Windows virtual machine;
- a Linux virtual machine;
- Wireshark;
- Sysmon;
- Splunk Free or a trial environment;
- Wazuh;
- sample logs from reputable training sources.

Do not expose intentionally vulnerable systems directly to the public internet.

## Project Status

This project is under active development.

- [x] Repository structure
- [x] Initial README
- [ ] Core handbook chapters
- [ ] Diagrams
- [ ] Detection examples
- [ ] Hands-on labs
- [ ] Cheat sheet
- [ ] Final review and references

See the repository issues and commit history for development progress.

## Documentation Principles

The handbook follows these principles:

- practical before overly theoretical;
- beginner-friendly but technically accurate;
- official and primary sources preferred;
- commands and detections explained, not merely copied;
- defensive and authorised use only;
- references provided for externally derived information.

## Ethical Use

This repository is intended exclusively for education, defensive security, authorised investigation, and controlled laboratory practice.

Never access, scan, monitor, exploit, or modify a system without explicit permission. The reader is responsible for complying with applicable laws, organisational policies, and professional ethical standards.

## Contributing

Suggestions, corrections, new lab ideas, and detection improvements are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before proposing a change.

## License

The educational content and code examples in this repository are released under the [MIT License](LICENSE), unless a file states otherwise.

## Disclaimer

This handbook does not replace vendor documentation, organisational procedures, legal advice, or professional incident-response guidance. Tools, platforms, techniques, and standards evolve continuously; readers should verify critical information against current official sources.

## Author

Created as a cybersecurity learning and portfolio project.

Add your name, programme, institution, and LinkedIn profile here if appropriate.
