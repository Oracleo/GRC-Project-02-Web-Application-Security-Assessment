# 1. Executive Summary

**Date of Assessment:** February 19, 2026
**Conducted By:** [Your Name]
**Assessment Type:** Manual Web Application Security Assessment (Unauthenticated & Authenticated)
**Target Application:** Public-Facing Customer Self-Service Portal (DVWA Simulation)

## Situation Overview
A manual security assessment was conducted on the organization's web application to evaluate the efficacy of existing application security controls. The assessment utilized the OWASP Web Security Testing Guide (WSTG) as the framework of choice. The application was tested for common vulnerabilities in the OWASP Top 10 (2021), including injection flaws, authentication weaknesses, and broken access controls.

## Key Findings
The assessment identified **4 critical and high-severity vulnerabilities**.
*   **P1 - SQL Injection (CVSS 9.8):** Confirmed exploitation leading to full database extraction of user records, including PII.
*   **P2 - Brute Force / Weak Authentication (CVSS 7.5):** Complete absence of rate limiting or account lockout, with credentials transmitted in plaintext via URL (GET request), exposing them to server logs and network sniffing.
*   **P2 - Reflected Cross-Site Scripting (XSS) (CVSS 7.3):** Confirmed injection of malicious JavaScript, allowing an attacker to steal session cookies and impersonate users.
*   **P3 - Cross-Site Request Forgery (CSRF) (CVSS 6.5):** Password change functionality is unprotected, allowing attackers to silently reset user passwords via malicious links.

## Strategic Recommendations
1.  **Immediate Secure Coding Overhaul:** Implement parameterized queries (Prepared Statements) to eliminate SQLi; introduce output encoding (`htmlspecialchars`) to eliminate XSS. (Cost: ~4 developer hours).
2.  **Hardening of Authentication:** Enforce rate limiting, account lockout policies, CAPTCHA, and migrate credential submissions to HTTP POST with HTTPS-only transmission.
3.  **SDLC Integration:** Mandate the inclusion of Anti-CSRF tokens for all state-changing operations. Introduce Static Application Security Testing (SAST) to prevent these classes of bugs from reaching production.
4.  **Technical Debt Remediation:** Move away from legacy PHP/MySQL patterns to modern frameworks that automatically handle input sanitization and CSRF protection.

## Conclusion
The target application faces severe security deficiencies. The 4 identified vulnerabilities compromise the confidentiality and integrity of customer data. **Failure to remediate the SQL Injection (P1) finding within 24 hours poses an immediate risk of a reportable GDPR data breach.**
