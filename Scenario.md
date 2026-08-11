# Incident Scenario

> This is a fictional cybersecurity incident used for a SOC incident-response portfolio project.

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


