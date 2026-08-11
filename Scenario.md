# Incident Scenario

> A simulated phishing incident designed to demonstrate practical SOC investigation and incident response skills.

## Organization

**Company:** TechCorp Solutions  
**Industry:** SaaS  
**Company Size:** Approximately 200 employees  

## What Happened

| Time | Event |
|------|-------|
| 9:00 AM | Employee Sarah Chen (Marketing) receives a phishing email with the subject "Action Required: Verify Your Account". The email contains a link to `techcorp-login.malicioussite.com`. |
| 9:15 AM | Sarah clicks the link and enters her corporate credentials on the fake login page. |
| 9:32 AM | The attacker uses Sarah's stolen credentials to access the corporate VPN from IP `185.220.101.42`. |
| 9:45 AM | The attacker accesses Sarah's email and forwards an HR portal password reset email to `recovery-techcorp@protonmail.com`. |
| 10:05 AM | The attacker uses VPN access to browse the HR and Finance internal file shares. |
| 10:22 AM | The attacker downloads 47 files (approximately 12 MB) from the HR compensation directory. |
| 10:30 AM | The SOC SIEM generates an anomalous VPN login alert for Sarah's account. |
| 10:35 AM | SOC investigation begins and confirms Sarah is in the office and not travelling. |
| 10:40 AM | Sarah's VPN access is disabled and a password reset is enforced. |
| 10:45 AM | The unauthorized session terminates. |
| 11:00 AM | Full incident investigation begins. |

---

## Known IOCs (Indicators of Compromise)

| Type | Value | Context |
|------|-------|---------|
| IP Address | `185.220.101.42` | Attacker's VPN source IP |
| Domain | `techcorp-login.malicioussite.com` | Phishing page |
| Email | `recovery-techcorp@protonmail.com` | Attacker's email used for forwarded resets |
| Email Subject | `"Action Required: Verify Your Account"` | Phishing email subject |
| File Hash (phishing page kit) | `SHA256: a1b2c3d4e5f6...deadbeef` | Phishing kit hash (from URL scan) |




