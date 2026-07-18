# 12. OWASP Top 10 Mapping

## Purpose

This document maps the identified web application vulnerabilities to the OWASP Top 10 (2021), MITRE ATT&CK framework, Common Weakness Enumeration (CWE), and Common Vulnerability Scoring System (CVSS). The objective is to demonstrate structured risk analysis, industry-standard classification, and alignment with secure software development practices.

---

## Mapping Summary

| Finding | OWASP Top 10 (2021) | CWE | MITRE ATT&CK | CVSS v3.1 | Business Risk |
|----------|---------------------|-----|---------------|-----------|---------------|
| SQL Injection | A03:2021 – Injection | CWE-89 | T1190 - Exploit Public-Facing Application | Critical | Unauthorized database access, data theft |
| Cross-Site Scripting (XSS) | A03:2021 – Injection | CWE-79 | T1059 - Command and Scripting Interpreter | High | Session hijacking, credential theft |
| Command Injection | A03:2021 – Injection | CWE-77 | T1059 - Command and Scripting Interpreter | Critical | Remote code execution |
| Weak Authentication | A07:2021 – Identification and Authentication Failures | CWE-287 | T1110 - Brute Force | High | Unauthorized account access |
| Missing Input Validation | A04:2021 – Insecure Design | CWE-20 | T1190 | Medium | Application abuse |
| Information Disclosure | A01:2021 – Broken Access Control / A05:2021 – Security Misconfiguration | CWE-200 | T1087 - Account Discovery | Medium | Sensitive information exposure |

> **Note:** Remove any findings from this table that were not identified during your assessment.

---

# Detailed Mapping

---

## Finding 1 – SQL Injection

### Description

Improper input validation allows attacker-controlled SQL queries to be executed against the backend database.

### OWASP Category

A03:2021 – Injection

### CWE

CWE-89 – Improper Neutralization of Special Elements used in an SQL Command

### MITRE ATT&CK

T1190 – Exploit Public-Facing Application

### Business Impact

- Unauthorized database access
- Exposure of confidential employee records
- Regulatory compliance violations
- Possible financial penalties

### Recommended Controls

- Parameterized queries
- Prepared statements
- Stored procedures
- Input validation
- Least privilege database accounts

---

## Finding 2 – Cross-Site Scripting (XSS)

### Description

User-supplied input is reflected without proper output encoding.

### OWASP Category

A03:2021 – Injection

### CWE

CWE-79 – Cross-site Scripting

### MITRE ATT&CK

T1059 – Command and Scripting Interpreter

### Business Impact

- Session hijacking
- Credential theft
- Client-side malware delivery
- Loss of user trust

### Recommended Controls

- Output encoding
- Input validation
- Content Security Policy (CSP)
- Secure cookie configuration

---

## Finding 3 – Command Injection

### Description

The application executes operating system commands using untrusted user input.

### OWASP Category

A03:2021 – Injection

### CWE

CWE-77 – Command Injection

### MITRE ATT&CK

T1059 – Command and Scripting Interpreter

### Business Impact

- Remote code execution
- Complete server compromise
- Data destruction
- Service disruption

### Recommended Controls

- Avoid system command execution
- Allow-list input validation
- Principle of least privilege
- Application sandboxing

---

## Finding 4 – Weak Authentication

### Description

Authentication controls permit weak credentials or insufficient verification mechanisms.

### OWASP Category

A07:2021 – Identification and Authentication Failures

### CWE

CWE-287 – Improper Authentication

### MITRE ATT&CK

T1110 – Brute Force

### Business Impact

- Unauthorized account access
- Privilege abuse
- Data compromise
- Account takeover

### Recommended Controls

- Multi-Factor Authentication (MFA)
- Strong password policy
- Account lockout
- Password hashing
- Login monitoring

---

## Finding 5 – Information Disclosure

### Description

The application exposes unnecessary system or application information to unauthenticated users.

### OWASP Category

A05:2021 – Security Misconfiguration

### CWE

CWE-200 – Exposure of Sensitive Information

### MITRE ATT&CK

T1087 – Account Discovery

### Business Impact

- Intelligence gathering
- Increased attack surface
- Targeted exploitation

### Recommended Controls

- Disable verbose error messages
- Remove debug information
- Secure server configuration
- Review application responses

---

# OWASP Coverage Summary

| OWASP Category | Addressed |
|----------------|-----------|
| A01 Broken Access Control | Partial |
| A02 Cryptographic Failures | Not Tested |
| A03 Injection | Yes |
| A04 Insecure Design | Partial |
| A05 Security Misconfiguration | Yes |
| A06 Vulnerable Components | Not Tested |
| A07 Identification and Authentication Failures | Yes |
| A08 Software and Data Integrity Failures | Not Tested |
| A09 Logging and Monitoring Failures | Not Tested |
| A10 Server-Side Request Forgery | Not Tested |

---

# Overall Assessment

The assessment identified several vulnerabilities that align with the OWASP Top 10 (2021), particularly within the **Injection**, **Authentication**, and **Security Misconfiguration** categories. These findings highlight the importance of secure coding practices, robust authentication mechanisms, comprehensive input validation, and continuous security testing throughout the Software Development Life Cycle (SDLC).

Implementing the recommended controls would significantly reduce the application's attack surface and improve its security posture while supporting compliance with ISO/IEC 27001, the NIST Cybersecurity Framework (CSF), and OWASP Application Security Verification Standard (ASVS).
