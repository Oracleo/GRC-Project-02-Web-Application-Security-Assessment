# 9. MITRE ATT&CK Mapping

Mapping our web application findings to MITRE ATT&CK allows us to visualize exactly how a real-world threat actor would chain these vulnerabilities together to breach the organization.

## Tactical Kill-Chain Mapping

| Vulnerability | MITRE Tactic | MITRE Technique ID | Technique Name | Adversary Action Enabled |
|:---|:---|:---|:---|:---|
| **SQL Injection** | **TA0001 (Initial Access)** | **T1190** | Exploit Public-Facing Application | The attacker gains a foothold by utilizing SQLi to bypass login entirely and retrieve credentials from the database. |
| **Brute Force / No Rate Limit** | **TA0006 (Credential Access)** | **T1110.001** | Brute Force: Password Guessing | The attacker runs automated dictionary attacks against the login portal to discover valid user passwords. |
| **Cross-Site Scripting (XSS)** | **TA0002 (Execution)** | **T1059.007** | Command and Scripting Interpreter: JavaScript | The attacker executes malicious JavaScript in the victim's browser. (This can be chained with **T1539 - Steal Web Session Cookie** under **TA0006** to harvest session tokens). |
| **Cross-Site Request Forgery (CSRF)** | **TA0004 (Privilege Escalation)** | **T1548** | Abuse Elevation Control Mechanism | An attacker forges a request to silently change the admin's password without authorization, bypassing normal access controls and elevating their privileges. |

## Attack Chain Scenario (The "Real World" Threat)
1.  **Reconnaissance (TA0043):** Attacker discovers the application is running on a vulnerable PHP 8.x stack through Burp Suite fingerprinting.
2.  **Initial Access (TA0001 - T1190):** Attacker executes a SQL Injection (`1' OR '1'='1`) on the login endpoint, bypassing authentication and dumping the `users` table, revealing hashed passwords.
3.  **Credential Access & Privilege Escalation (TA0006 & TA0004):** Using a brute force attack against the admin login (T1110.001), the attacker cracks the admin password. Once logged in as admin, the attacker uses a CSRF attack (T1548) to change the admin's password, effectively locking out the real admin and creating a backdoor account via privilege escalation.
4.  **Persistence (TA0003):** The XSS vulnerability (T1059.007) is used to embed a keylogger that steals session tokens (T1539) of other users, ensuring long-term access to the organization.

**GRC Recommendation:** To disrupt this kill-chain, implement **Web Application Firewall (WAF) rules** (to block SQLi and XSS patterns), implement **Multi-Factor Authentication** (to neutralize brute-force), and adopt **Zero-Trust Architecture** for all session tokens.
