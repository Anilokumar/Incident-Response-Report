# Incident Scenario — TechCorp Solutions

> This case study recreates a realistic SOC incident involving phishing,
> credential compromise, unauthorized VPN access, and data exposure.
> The organization and environment are fictional, while the investigation
> follows standard incident-response practices.

## Organization

**Organization:** TechCorp Solutions  
**Industry:** SaaS  
**Environment Size:** Approximately 200 employees  
**Affected User:** Sarah Chen  
**Department:** Marketing  

---

## Incident Overview

At 9:00 AM, Sarah Chen received a phishing email with the subject
"Action Required: Verify Your Account." The email contained a link to
`techcorp-login.malicioussite.com`, a fraudulent login page designed
to capture corporate credentials.

At 9:15 AM, Sarah entered her corporate credentials into the fraudulent
login page. The stolen credentials were later used to establish an
unauthorized corporate VPN session from IP address `185.220.101.42`.

Following VPN access, Sarah's corporate email account was accessed and
an HR portal password-reset email was forwarded to the external address
`recovery-techcorp@protonmail.com`.

The unauthorized session was then used to browse internal HR and Finance
file shares. At 10:22 AM, 47 files totaling approximately 12 MB were
downloaded from the HR compensation directory.

At 10:30 AM, an anomalous VPN login alert triggered an investigation.
Sarah was confirmed to be in the office and not travelling. VPN access
was subsequently disabled, a password reset was enforced, and the
unauthorized session was terminated.

---

## Initial Incident Timeline

| Time | Event |
|------|-------|
| 9:00 AM | Sarah Chen receives a phishing email with the subject "Action Required: Verify Your Account" containing a link to `techcorp-login.malicioussite.com`. |
| 9:15 AM | Sarah clicks the phishing link and enters her corporate credentials on the fraudulent login page. |
| 9:32 AM | The stolen credentials are used to access the corporate VPN from IP `185.220.101.42`. |
| 9:45 AM | Sarah's corporate email is accessed and an HR portal password-reset email is forwarded to `recovery-techcorp@protonmail.com`. |
| 10:05 AM | The VPN session is used to browse `\\fileserver\HR\compensation\` and `\\fileserver\Finance\Q1-reports\`. |
| 10:22 AM | 47 files (approximately 12 MB) are downloaded from the HR compensation directory. |
| 10:30 AM | An anomalous VPN login alert is generated for Sarah's account due to a new device and unusual geolocation. |
| 10:35 AM | Investigation confirms Sarah is in the office and is not travelling. |
| 10:40 AM | Sarah's VPN access is disabled and a password reset is enforced. |
| 10:45 AM | The unauthorized VPN session terminates. |
| 11:00 AM | A full incident investigation begins. |

---

## Initial Indicators of Compromise (IOCs)

| Type | Value | Context |
|------|-------|---------|
| IP Address | `185.220.101.42` | Source IP associated with the unauthorized VPN login |
| Domain | `techcorp-login.malicioussite.com` | Domain associated with the phishing login page |
| Email Address | `recovery-techcorp@protonmail.com` | External address used for forwarding the HR password-reset email |
| Email Subject | `Action Required: Verify Your Account` | Subject used in the phishing email |
| File Hash | `SHA256: a1b2c3d4e5f6...deadbeef` | Phishing-kit hash associated with the simulated incident |

---

## Investigation Scope

The investigation focuses on reconstructing the attack timeline,
identifying indicators of compromise, analyzing attacker activity,
mapping observed behavior to the MITRE ATT&CK framework, and documenting
appropriate containment, eradication, and security recommendations.
