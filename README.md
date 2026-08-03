# SOC Analyst Handbook

[English](README.md) | [Magyar](README.hu.md)

> A bilingual practical handbook for aspiring SOC analysts, covering security operations, networking, operating-system security, log analysis, SIEM, threat intelligence, MITRE ATT&CK, incident response, malware, and detection engineering.

## Overview

The **SOC Analyst Handbook** is an educational and portfolio-oriented documentation project for cybersecurity students and aspiring blue team professionals.

The repository presents the same core material in two languages:

- [English documentation](docs/en/)
- [Hungarian documentation](docs/hu/)

The English version supports professional language development and makes the project suitable for an international portfolio. The Hungarian version supports clear understanding of the concepts and provides an accessible learning resource.

## Intended Audience

This handbook is intended for cybersecurity students, aspiring SOC analysts, junior blue team professionals, IT professionals transitioning into cybersecurity, and anyone interested in the foundations of security operations.

## Learning Objectives

After working through the handbook, readers should be able to:

1. explain the purpose and basic structure of a Security Operations Center;
2. describe common Tier 1, Tier 2, and Tier 3 analyst responsibilities;
3. understand essential networking protocols and traffic patterns;
4. identify important Windows and Linux security events;
5. interpret common security logs and recognise suspicious activity;
6. explain the role of SIEM platforms in security monitoring;
7. distinguish indicators of compromise from attacker behaviours;
8. use MITRE ATT&CK to classify observed activity;
9. describe the main stages of incident response;
10. understand the foundations of malware analysis and detection engineering.

## Repository Structure

```text
SOC-Analyst-Handbook/
├── README.md
├── README.hu.md
├── LICENSE
├── CONTRIBUTING.md
├── SECURITY.md
└── docs/
    ├── en/
    └── hu/
```

## Handbook Chapters

| No. | Chapter | Main topics |
|---:|---|---|
| 01 | Introduction to Security Operations | SOC purpose, blue team, analyst roles, NOC vs SOC |
| 02 | How a SOC Works | People, processes, technology, alerts and escalation |
| 03 | Network Fundamentals | OSI, TCP/IP, DNS, HTTP(S), DHCP, ARP and ICMP |
| 04 | Windows Security | Event Viewer, authentication, processes, services and PowerShell |
| 05 | Linux Security | Users, permissions, sudo, authentication logs, systemd and cron |
| 06 | Log Analysis | Windows, Sysmon, web server, firewall and authentication logs |
| 07 | SIEM Fundamentals | Splunk, Microsoft Sentinel, Wazuh and QRadar |
| 08 | Cyber Threat Intelligence | IOC, IOA, TTP, CVE, CVSS, STIX and TAXII |
| 09 | MITRE ATT&CK | Tactics, techniques, mapping and investigation support |
| 10 | Incident Response | Preparation, detection, response, recovery and improvement |
| 11 | Malware Basics | Trojans, worms, RATs, rootkits, ransomware and spyware |
| 12 | Detection Engineering | Sigma, YARA, KQL and SPL concepts |
| 13 | Practical Examples | Guided analysis scenarios and documentation examples |
| 14 | SOC Analyst Cheat Sheet | Event IDs, ports, commands, queries and investigation prompts |
| 15 | References | Standards, official documentation and further reading |

## Documentation Approach

The handbook follows these principles:

- beginner-friendly but technically accurate;
- practical explanations supported by examples;
- consistent structure in both languages;
- official and primary sources preferred;
- technical terms explained in context;
- defensive and authorised use only;
- references provided for externally derived information.

## Project Status

- [x] Repository structure
- [x] English and Hungarian README files
- [x] Bilingual chapter structure
- [ ] Complete Hungarian chapters
- [ ] Complete English chapters
- [ ] Technical review
- [ ] Language review
- [ ] Final references

## Ethical Use

This repository is intended exclusively for education, defensive security, authorised investigation, and controlled learning environments.

Never access, monitor, scan, or modify a system without explicit permission.

## Contributing

Suggestions and corrections are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before proposing a change.

## License

The educational content in this repository is released under the [MIT License](LICENSE), unless a file states otherwise.

## Disclaimer

This handbook does not replace vendor documentation, organisational procedures, legal advice, or professional incident-response guidance. Cybersecurity tools, platforms, techniques, and standards evolve continuously; readers should verify critical information against current official sources.

## Author

Created by Lea Varga as a cybersecurity learning and portfolio project.
