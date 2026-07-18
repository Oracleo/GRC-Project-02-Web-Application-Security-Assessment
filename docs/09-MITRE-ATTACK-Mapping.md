# 9. MITRE ATT&CK Threat Actor Mapping

Mapping our web application findings to MITRE ATT&CK allows us to visualize exactly how a real-world threat actor would chain these vulnerabilities together to breach the organization.

## Tactical Kill-Chain Mapping

| Vulnerability | MITRE Tactic | MITRE Technique ID | Technique Name | Adversary Action Enabled |
|:---|:---|:---|:---|:---|
| **SQL Injection** | **TA0001 (Initial Access)** | **T1190** | Exploit Public-Facing Application | The attacker gains a foothold by utilizing SQLi to bypass login entirely and retrieve credentials from the database. |
| **Brute Force / No Rate Limit** | **TA0006 (Credential Access)** | **T1110.001** | Brute Force: Password Guessing | The attacker runs automated dictionary attacks against the login portal to discover valid user passwords. |
| **Cross-Site Scripting (XSS)** | **TA0006 (Credential Access)** | **T1059.007** | Command and Scripting Interpreter: JavaScript | The attacker injects a malicious payload to steal session cookies (Session Hijacking). |
| **Cross-Site Request Forgery (CSRF)** | **TA0004 (Privilege Escalation)** | **T1548** | Abuse Elevation Control Mechanism | An attacker forces an authenticated Admin to silently change their password, allowing the attacker to take over admin accounts. |

## Attack Chain Scenario (The "Real World" Threat)
1.  **Reconnaissance (TA0043):** Attacker discovers the application is running on a vulnerable PHP 8.x stack through Burp Suite fingerprinting.
2.  **Initial Access (TA0001 - T1190):** Attacker executes a SQL Injection (`1' OR '1'='1`) on the login endpoint, bypassing authentication and dumping the `users` table, revealing hashed passwords.
3.  **Privilege Escalation (TA0004):** Using a brute force attack against the admin login (T1110.001), the attacker cracks the admin password.
4.  **Persistence / Lateral Movement:** Once logged in as admin, the attacker uses a CSRF attack (T1185) to create a backdoor admin account, ensuring they never lose access.
5.  **Exfiltration (TA0010):** The attacker utilizes the XSS vulnerability (T1059.007) to embed a keylogger that steals session tokens of other users, extracting PII data for identity theft.

**GRC Recommendation:** To disrupt this kill-chain, implement **Web Application Firewall (WAF) rules** (to block SQLi and XSS patterns), implement **Multi-Factor Authentication** (to neutralize brute-force), and adopt **Zero-Trust Architecture** for all session tokens.
