# Incident Response Report: Phishing-Led Account Compromise and Data Exfiltration

**Analyst:** Anil Kumar Ramesh  
**Organization:** TechCorp Solutions (Fictional)  
**Incident Type:** Phishing / Credential Compromise / Data Exfiltration  
**Severity:** High  
**Status:** Contained  
**Report Date:** 12 August 2026  

---

## 1. Executive Summary

TechCorp Solutions identified a phishing attack that resulted in the compromise of employee Sarah Chen's corporate credentials. The attacker used the stolen credentials to gain unauthorized VPN access, access internal HR and Finance resources, and download **47 files (12 MB)** from the HR compensation directory.

The incident was detected through anomalous VPN activity. The compromised account was contained by disabling Sarah's VPN access, forcing a password reset, and terminating the unauthorized session.

---
## 2. Incident Timeline

The following timeline reconstructs the incident from the initial phishing email through unauthorized access, data collection, detection, and containment.

| Time         | Event                                                                                                                                                     | Evidence Source                            | Severity | Investigation Notes                                                                                                                                                                               |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **9:00 AM**  | Sarah Chen receives a phishing email with the subject **"Action Required: Verify Your Account"** containing a link to `techcorp-login.malicioussite.com`. | Email Gateway Logs                         | Medium   | The message contains a suspicious external domain designed to imitate a legitimate corporate login page and obtain user credentials.                                                              |
| **9:15 AM**  | Sarah clicks the phishing link and enters her corporate credentials into the fraudulent login page.                                                       | Web/Proxy Logs / User Investigation        | High     | The interaction results in credential exposure, allowing the attacker to potentially authenticate to corporate services as Sarah.                                                                 |
| **9:32 AM**  | Sarah's stolen credentials are used to establish a successful corporate VPN session from IP address `185.220.101.42`.                                     | VPN Gateway / Authentication Logs          | High     | The login originates from an unusual location and device. Later user verification confirms that Sarah did not initiate the connection.                                                            |
| **9:45 AM**  | Sarah's corporate email is accessed without authorization, and an HR portal password-reset email is forwarded to `recovery-techcorp@protonmail.com`.      | Email Audit Logs                           | High     | Forwarding the password-reset message to an external address indicates an attempt to extend unauthorized access to the HR portal.                                                                 |
| **10:05 AM** | The unauthorized VPN session accesses internal file shares, including `\\fileserver\HR\compensation\` and `\\fileserver\Finance\Q1-reports\`.             | File Server Audit Logs                     | High     | Access to HR and Finance directories indicates internal resource discovery and access to sensitive business information.                                                                          |
| **10:22 AM** | Sarah's compromised account downloads **47 files (12 MB)** from the HR compensation directory.                                                            | File Server Audit Logs                     | High     | The successful download confirms unauthorized collection of sensitive HR data. Available evidence confirms the Finance directory was accessed but does not confirm files were downloaded from it. |
| **10:30 AM** | An anomalous VPN login alert is generated for Sarah's account due to a new device and unusual geolocation.                                                | SIEM Alert                                 | High     | The alert identifies activity inconsistent with Sarah's expected login behavior and becomes the primary detection point for the incident.                                                         |
| **10:35 AM** | The investigation confirms that Sarah is in the office and is not travelling.                                                                             | User Verification / Incident Investigation | High     | Sarah's confirmed physical location conflicts with the VPN activity, providing strong evidence that the VPN session is unauthorized.                                                              |
| **10:40 AM** | Sarah's VPN access is disabled and a password reset is enforced.                                                                                          | Identity / VPN Administration Logs         | High     | These containment actions prevent continued use of the compromised credentials and restrict the attacker's access to corporate resources.                                                         |
| **10:45 AM** | The unauthorized VPN session is terminated.                                                                                                               | VPN Gateway Logs                           | High     | Termination of the session removes the attacker's immediate VPN access to the internal environment.                                                                                               |
| **11:00 AM** | A full incident investigation begins to determine the scope and impact of the compromise.                                                                 | Incident Response Records                  | High     | Further investigation is required to identify additional affected systems, accounts, data exposure, and indicators of compromise.                                                                 |

### Timeline Analysis

The incident progressed from phishing and credential theft to unauthorized VPN access, email-account misuse, internal file-share access, and the collection of sensitive HR information.

The first confirmed unauthorized VPN session was established at **9:32 AM** and terminated at **10:45 AM**, resulting in approximately **73 minutes of confirmed unauthorized VPN access**.

The incident was detected at **10:30 AM** following an anomalous VPN login alert. After confirming that Sarah was not responsible for the suspicious connection, containment actions were initiated at **10:40 AM**, approximately **10 minutes after detection**.

## 3. Indicators of Compromise (IOCs)

The following indicators were identified during the investigation and can be used to support threat hunting, detection, and blocking activities across the environment.

| IOC Type          | Indicator                              | Context                                                                                      | Recommended Action                                                                                                   |
| ----------------- | -------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **IP Address**    | `185.220.101.42`                       | Source IP associated with the unauthorized VPN login to Sarah's account.                     | Search authentication and VPN logs for additional connections from the IP and block where appropriate.               |
| **Domain**        | `techcorp-login.malicioussite.com`     | Fraudulent login domain used to capture Sarah's corporate credentials.                       | Block the domain through web filtering and search proxy/DNS logs for other users who accessed it.                    |
| **Email Address** | `recovery-techcorp@protonmail.com`     | External email address used to receive the forwarded HR portal password-reset message.       | Search email logs for communication or forwarding activity involving the address and block where appropriate.        |
| **Email Subject** | `Action Required: Verify Your Account` | Subject line associated with the phishing campaign targeting Sarah.                          | Search email gateway logs for other employees who received messages with the same or similar subject.                |
| **File Hash**     | `SHA256: a1b2c3d4e5f6...deadbeef`      | Simulated SHA-256 hash associated with the phishing kit referenced in the incident scenario. | Search available security telemetry for matches and add the hash to relevant detection/block lists where applicable. |

### IOC Analysis

The identified indicators should be used to determine whether the phishing campaign affected additional employees or systems. Particular attention should be given to authentication activity involving `185.220.101.42` and web or DNS activity involving `techcorp-login.malicioussite.com`.

A broader search across VPN, email, proxy, DNS, and authentication logs would help determine whether Sarah Chen was the only targeted or compromised employee.

