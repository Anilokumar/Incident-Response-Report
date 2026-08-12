# Incident Response Investigation — Phishing Account Compromise

Conducted a simulated SOC investigation of a phishing attack involving credential theft, unauthorized VPN access, and data exfiltration, with MITRE ATT&amp;CK mapping and incident response recommendations

## Project Overview

Conducted a simulated SOC investigation of a phishing attack involving credential theft, unauthorized VPN access, internal resource access, and data exfiltration.

The investigation involved reconstructing the attack timeline, identifying Indicators of Compromise (IOCs), mapping attacker behaviour to the MITRE ATT&CK framework, and developing containment, eradication, and security recommendations.

> **Disclaimer:** TechCorp Solutions and the incident environment are fictional. This project was developed to demonstrate practical SOC and incident-response investigation skills.

---

## Incident Summary

A TechCorp employee was targeted by a phishing email containing a fraudulent login page designed to capture corporate credentials.

The stolen credentials were used to establish unauthorized VPN access to the corporate environment. The compromised account was then used to access corporate email and browse sensitive HR and Finance resources.

During the incident, **47 files totaling 12 MB** were downloaded from the HR compensation directory.

An anomalous VPN login alert triggered the investigation, leading to containment of the compromised account and termination of the unauthorized session.

---

## Key Findings

- Employee credentials were compromised through a phishing login page.
- Stolen credentials were used to establish unauthorized VPN access.
- The compromised account was used to access corporate email.
- Internal HR and Finance file shares were accessed.
- **47 HR files (12 MB)** were downloaded.
- An unusual VPN login triggered the security investigation.
- The compromised account was contained through VPN restriction, password reset, and session termination.

---

## Skills Demonstrated

- SOC Investigation
- Incident Response
- Phishing Analysis
- Log Analysis
- Incident Timeline Reconstruction
- Indicator of Compromise (IOC) Analysis
- MITRE ATT&CK Mapping
- Account Compromise Investigation
- Threat Hunting
- Containment and Eradication
- Security Recommendations

---

## MITRE ATT&CK Mapping

| Technique | MITRE ATT&CK ID |
|---|---|
| Phishing: Spearphishing Link | `T1566.002` |
| Valid Accounts | `T1078` |
| Email Collection | `T1114` |
| Remote Services | `T1021` |
| File and Directory Discovery | `T1083` |
| Data from Local System | `T1005` |
| Exfiltration Over Alternative Protocol | `T1048` |

---

## Investigation Process

The investigation followed a structured SOC incident-response workflow:

**Phishing Detection → Account Compromise Analysis → Timeline Reconstruction → IOC Analysis → MITRE ATT&CK Mapping → Containment → Eradication → Security Recommendations**

---

## Repository Structure

```text
incident-response-report/
│
├── README.md
├── scenario.md
└── incident-response-report.md
...

### File Descriptions

- **`README.md`** — Provides an overview of the project, key findings, investigation process, and skills demonstrated.
- **`scenario.md`** — Contains the simulated incident scenario, initial timeline, and known Indicators of Compromise (IOCs).
- **`incident-response-report.md`** — Contains the complete SOC investigation, including timeline analysis, IOC analysis, MITRE ATT&CK mapping, containment, eradication, and security recommendations.

---

## Key Takeaways

This project strengthened my understanding of how SOC analysts investigate phishing-led account compromises by correlating authentication, VPN, email, and file-access activity.

The investigation reinforced the importance of distinguishing confirmed evidence from assumptions, analyzing multiple log sources, identifying indicators of compromise, and recommending appropriate containment and remediation actions.

---

## Project Note

This project is based on a fictional organization and simulated security incident. The investigation follows realistic SOC and incident-response practices.

---

## Author

**Anil Kumar Ramesh**

Cybersecurity student focused on SOC operations, incident response, network security, and threat analysis.
