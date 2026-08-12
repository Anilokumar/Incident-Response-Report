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

## 4. Attack Analysis — MITRE ATT&CK Mapping

The observed attacker activity was mapped to the MITRE ATT&CK framework to identify the techniques used throughout the incident.

| Attack Phase                   | Technique                              | MITRE ATT&CK ID | Analysis                                                                                                                                                                 |
| ------------------------------ | -------------------------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Initial Access**             | Phishing: Spearphishing Link           | `T1566.002`     | The attacker sent Sarah a phishing email containing a link to a fraudulent corporate login page designed to steal her credentials.                                       |
| **Credential / Account Abuse** | Valid Accounts                         | `T1078`         | After obtaining Sarah's credentials, the attacker used the legitimate account credentials to authenticate to the corporate VPN.                                          |
| **Email Access**               | Email Collection                       | `T1114`         | The attacker accessed Sarah's corporate mailbox and interacted with an HR portal password-reset email.                                                                   |
| **Remote Access**              | Remote Services                        | `T1021`         | The compromised account was used to establish remote access to the corporate environment through the VPN.                                                                |
| **Discovery**                  | File and Directory Discovery           | `T1083`         | After obtaining VPN access, the attacker browsed internal HR and Finance file shares to identify potentially valuable information.                                       |
| **Collection**                 | Data from Local System                 | `T1005`         | The attacker collected 47 files totaling 12 MB from the HR compensation directory using Sarah's compromised account.                                                     |
| **Exfiltration**               | Exfiltration Over Alternative Protocol | `T1048`         | The incident scenario indicates that sensitive HR data was downloaded through the unauthorized remote session, representing data removal from the corporate environment. |

### Attack Chain Analysis

The attack began with a phishing email containing a link to a fraudulent login page. Sarah entered her corporate credentials into the phishing site, allowing the attacker to obtain valid account credentials.

The attacker then used Sarah's credentials to establish unauthorized VPN access and gain entry to internal corporate resources. After accessing Sarah's email account, the attacker attempted to extend access by forwarding an HR portal password-reset message to an external email address.

## 5. Containment and Eradication

### 5.1 Containment Actions

Once the unauthorized activity was confirmed, immediate containment actions were taken to prevent further access to TechCorp's environment.

| Action                                                   | Purpose                                                                            | Status      |
| -------------------------------------------------------- | ---------------------------------------------------------------------------------- | ----------- |
| Disabled Sarah's VPN access                              | Prevent further remote access using the compromised account                        | Completed   |
| Forced a password reset                                  | Invalidate the stolen corporate password                                           | Completed   |
| Terminated the active VPN session                        | Remove the attacker's immediate access to internal resources                       | Completed   |
| Block attacker IP `185.220.101.42`                       | Prevent additional connection attempts from the identified source IP               | Recommended |
| Block `techcorp-login.malicioussite.com`                 | Prevent other employees from accessing the identified phishing site                | Recommended |
| Block and investigate `recovery-techcorp@protonmail.com` | Prevent further interaction with the external address associated with the incident | Recommended |

### 5.2 Eradication Actions

Following containment, additional actions should be performed to remove any remaining attacker access and determine whether the compromise extended beyond Sarah's account.

1. **Revoke active sessions and authentication tokens** associated with Sarah's account to ensure previously authenticated sessions cannot continue to be used.

2. **Review Sarah's email account** for malicious forwarding rules, inbox rules, delegated access, or other unauthorized configuration changes.

3. **Review HR portal activity** to determine whether the attacker successfully reset credentials or gained access to Sarah's HR account.

4. **Search VPN and authentication logs** for additional activity associated with `185.220.101.42` and Sarah's account.

5. **Search email gateway logs** to identify whether the phishing message was delivered to other TechCorp employees.

6. **Search proxy and DNS logs** for connections to `techcorp-login.malicioussite.com` to identify additional users who may have visited the phishing page.

7. **Review file server audit logs** to determine exactly which files and directories were accessed or downloaded during the unauthorized session.

8. **Reset any additional credentials** found to have been exposed or compromised during the investigation.

9. **Monitor Sarah's account** for additional abnormal authentication attempts following remediation.

### Containment Status

The immediate threat was contained when Sarah's VPN access was disabled, her password was reset, and the unauthorized VPN session was terminated at 10:45 AM. However, further investigation is required to confirm that no additional accounts, sessions, or systems were compromised.


Using the unauthorized VPN session, the attacker browsed internal HR and Finance directories and subsequently downloaded 47 files from the HR compensation directory. The activity was eventually detected through an anomalous VPN login alert and contained by the incident-response team.

## 6. Lessons Learned and Recommendations

The incident demonstrated that a successful phishing attack against a single employee account could provide an attacker with access to multiple corporate resources. Based on the investigation, the following security improvements are recommended.

| Area | Recommendation | Reason |
|---|---|---|
| Authentication | Enforce multi-factor authentication (MFA) for VPN, email, and other critical corporate services. | Stolen passwords alone should not be sufficient to access corporate resources. |
| Email Security | Strengthen email filtering and phishing detection for suspicious domains, links, and impersonation attempts. | The initial compromise began with a phishing email containing a fraudulent login link. |
| Web Security | Block known malicious domains and improve DNS/web filtering. | This can prevent users from accessing identified phishing infrastructure. |
| VPN Monitoring | Generate alerts for unusual geolocation, unknown devices, and abnormal VPN login behaviour. | The anomalous VPN login was the primary detection point in this incident. |
| Data Loss Prevention | Implement DLP controls and monitoring for unusual downloads of sensitive HR and Finance information. | The attacker successfully downloaded 47 sensitive HR files before the incident was detected. |
| Access Control | Review least-privilege permissions for sensitive HR and Finance file shares. | Users should only have access to information required for their job responsibilities. |
| Security Awareness | Conduct regular phishing-awareness training and simulated phishing exercises. | Employees should be able to recognize suspicious login pages, urgent requests, and unusual domains. |
| Incident Response | Develop and regularly test procedures for account compromise, phishing, and unauthorized remote access. | Clear procedures can reduce the time between detection, investigation, and containment. |
| Threat Hunting | Search historical VPN, authentication, email, DNS, proxy, and file-access logs using identified IOCs. | This helps determine whether additional users or systems were targeted or compromised. |

### Lessons Learned

The incident highlights the importance of layered security controls. Preventing phishing alone is not sufficient; organizations should combine strong authentication, access controls, monitoring, user awareness, and incident-response procedures.

The anomalous VPN login alert successfully identified suspicious activity, but sensitive HR files had already been accessed and downloaded before the alert was generated. Earlier detection of credential misuse and abnormal file-access behaviour could have reduced the impact of the incident.

## 7. Conclusion

The investigation determined that a phishing attack resulted in the compromise of Sarah Chen's corporate credentials and subsequent unauthorized access to TechCorp's environment. The attacker used the compromised account to establish a VPN session, access corporate email, browse sensitive HR and Finance resources, and download 47 files totaling 12 MB from the HR compensation directory.

The incident was detected through anomalous VPN activity and contained by disabling VPN access, forcing a password reset, and terminating the unauthorized session.

This investigation highlights the importance of strong authentication, phishing protection, continuous monitoring, least-privilege access, and effective incident-response procedures. The identified IOCs and MITRE ATT&CK mappings can also be used to support further threat hunting and detection activities.
