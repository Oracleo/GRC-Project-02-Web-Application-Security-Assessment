# Web Application Risk Assessment | OWASP Top 10 & CVSS Scoring

![Burp Suite](https://img.shields.io/badge/Tool-Burp%20Suite%20CE%20v2026.1.3-FF6633?style=for-the-badge&logo=burpsuite&logoColor=white)
![OWASP](https://img.shields.io/badge/Methodology-OWASP%20Top%2010-000000?style=for-the-badge&logo=owasp&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Platform-Kali%20Linux%202026-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![Findings](https://img.shields.io/badge/Findings-1%20Critical%20%7C%202%20High%20%7C%201%20Medium-FF0000?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-28A745?style=for-the-badge)
![Framework](https://img.shields.io/badge/Framework-ISO%2027001%20%7C%20NIST%20CSF-0057A8?style=for-the-badge)
![Scoring](https://img.shields.io/badge/Risk%20Scoring-CVSS%20v3.0-blueviolet?style=for-the-badge)

**A structured, end-to-end Web Application Risk Assessment simulating a real-world GRC engagement.** Conducted manually against DVWA using Burp Suite Community Edition. This project documents the complete GRC lifecycle—from scope definition and manual testing to executive reporting, compliance gap analysis, cost-benefit remediation planning, and residual risk acceptance.

---

## Project at a Glance

| Area | Details |
|:---|:---|
| **Risk Methodology** | Manual OWASP WSTG testing framework. CVSS v3.0 scoring + Cost-Benefit Analysis. |
| **Findings** | 4 vulnerabilities: **1 Critical (P1)** SQLi, 2 High (P2) XSS/Brute Force, 1 Medium (P3) CSRF. |
| **Regulatory Mapping** | Aligned to **ISO 27001** (Annex A), **NIST CSF**, **PCI DSS v4.0**, and **GDPR**. |
| **Key Deliverables** | Executive Summary, Risk Register, Compliance Gap Analysis, Remediation Tracker, Residual Risk Assessment, and Lessons Learned. |
| **Tools Used** | Burp Suite CE, OWASP Top 10, Kali Linux, DVWA. |

---

## Full Documentation Index (GRC Artifacts)

This repository is structured to mirror a professional GRC consultant's audit file.  
**Hiring managers:** Click any document below to see exactly how I translate raw technical findings into formal business risk.

| No. | Document | Core Purpose |
|:---:|:---|:---|
| **01** | `docs/01-Executive-Summary.md` | Non-technical overview for senior stakeholders (Board/CISO). |
| **02** | `docs/02-Executive-Dashboard.md` | Visual KPIs: High-level risk posture and compliance heatmap. |
| **03** | `docs/03-Scope-Methodology.md` | Formal Terms of Reference (ToR) defining the engagement rules and OWASP testing approach. |
| **04** | `docs/04-Assumed-Business-Context.md` | The **"story"** behind the asset: Fictional organizational profile, risk appetite, and industry scenario. |
| **05** | `docs/05-Risk-Register.md` | Detailed master risk register: CVSS, Likelihood, Impact, and P1–P4 priority scoring. |
| **06** | `docs/06-Remediation-Tracker.md` | Project management artifact tracking SLA dates, remediation costs, and financial cost-benefit analysis. |
| **07** | `docs/07-Compliance-Gap-Analysis.md` | Direct mapping of technical vulnerabilities to ISO 27001 Annex A, NIST CSF, PCI DSS, and GDPR controls. |
| **08** | `docs/08-Asset-Business-Criticality.md` | Deep dive on data sensitivity (PII/customer data) and operational criticality of the target application. |
| **09** | `docs/09-MITRE-ATTACK-Mapping.md` | Threat-informed defense mapping: Correlating vulnerabilities to real-world adversary TTPs (Tactics, Techniques, Procedures). |
| **10** | `docs/10-Residual-Risk-Assessment.md` | **Executive sign-off document:** Formal acceptance of risk remaining after implementing compensating controls. |
| **11** | `docs/11-Lessons-Learned.md` | Continual Improvement (ISO 27001 Clause 10.2): Post-engagement review identifying gaps and takeaways for future cycles. |

---

## Repository Artifacts & Raw Evidence

| Location | Description |
|:---|:---|
| **`artifacts/`** | Raw Burp Suite intercept logs, request/response dumps, and vulnerability exploitation evidence. |
| **`screenshots/`** | 23 annotated screenshots documenting the lab setup, Burp Suite intercepts, and vulnerability exploitation. |

## Screenshots Index (23 Image Evidence)

Below is the complete screenshot inventory documenting the entire assessment lifecycle — from Kali Linux setup and DVWA deployment, to Burp Suite interception, vulnerability discovery, and exploitation validation.

| No. | Filename | Description |
|---|----------|-------------|
| 01 | `GRC2_01_kali_ip_address.png` | Kali Linux IP address confirmation (`10.83.80.7`) via `ip a`. |
| 02 | `GRC2_02_apache_running.png` | Apache 2.4.66 web server service status — active and running. |
| 03 | `GRC2_03_mysql_running.png` | MariaDB 11.8.5 database service status — active and running. |
| 04 | `GRC2_04_mysql_database_setup.png` | MySQL database setup — DVWA database created and privileges granted. |
| 05 | `GRC2_05_dvwa_setup_page.png` | DVWA setup page — database connection successful, Create/Reset Database button. |
| 06 | `GRC2_06_dvwa_login_page.png` | DVWA login page — default credentials (`admin` / `password`). |
| 07 | `GRC2_06.1_dvwa_home_logged_in.png` | DVWA home page — logged in as admin, security level: Low. |
| 08 | `GRC2_07_burp_suite_launched.png` | Burp Suite Community Edition — launched and ready on port 8080. |
| 09 | `GRC2_08_firefox_proxy_config.png` | Firefox browser proxy configuration — pointing to `127.0.0.1:8080`. |
| 10 | `GRC2_09_burp_intercept_dvwa_request.png` | Burp Suite intercepting DVWA login request — traffic capture enabled. |
| 11 | `GRC2_10_dvwa_loaded_with_burp_proxy.png` | DVWA loaded successfully through Burp proxy — traffic flowing via intercept. |
| 12 | `GRC2_11_dvwa_security_level_low.png` | DVWA Security Level set to **Low** — all vulnerabilities enabled. |
| 13 | `GRC2_12_sql_injection_normal_test.png` | SQL Injection test — normal input (`1' OR '1'='1`) entered in User ID field. |
| 14 | `GRC2_13_sql_injection_exploit_success.png` | **Critical (P1):** SQL Injection successful — full user database dumped (admin, Gordon, etc.). |
| 15 | `GRC2_14_burp_sql_injection_request_analysis.png` | Burp request analysis — SQLi payload captured and analyzed. |
| 16 | `GRC2_15_xss_normal_test.png` | Reflected XSS test — normal input entered in vulnerable field. |
| 17 | `GRC2_16_xss_exploit_alert_popup.png` | **High (P2):** XSS exploitation successful — JavaScript alert popup (`alert('XSS')`). |
| 18 | `GRC2_17_burp_xss_request_analysis.png` | Burp request analysis — XSS payload in URL parameter captured. |
| 19 | `GRC2_18_brute_force_successful_login.png` | **High (P2):** Brute Force attack — successful login discovered (`admin` / `password`). |
| 20 | `GRC2_19_brute_force_failed_attempt.png` | Brute Force attack — failed login attempt captured in Burp intruder. |
| 21 | `GRC2_20_burp_brute_force_analysis.png` | Burp analysis — brute force attack with dictionary wordlist. |
| 22 | `GRC2_21_csrf_password_change_success.png` | **Medium (P3):** CSRF attack — password change request successful without anti-CSRF token. |
| 23 | `GRC2_22_burp_csrf_request_analysis.png` | Burp request analysis — CSRF password change request captured. |

> **Visual Audit Trail:** These 23 screenshots serve as the primary evidence artifact for this assessment. Together with the Burp Suite intercept logs and request/response dumps, they provide a complete, defensible audit trail for ISO 27001, PCI DSS, and GDPR compliance reviews.

---

## Lab Architecture & Tools

This assessment was performed in an isolated VirtualBox environment with a bridged network adapter to simulate a standard LAN-hosted web application.

```text
┌──────────────────────────────────────────────────────────────────────────────┐
│                     Windows 10 Host (Oracle VirtualBox)                      │
│                                                                              │
│  ┌───────────────────────────┐      ┌───────────────────────────┐            │
│  │ Firefox Browser           │────▶│ Burp Suite Community       │            │
│  │ Proxy: 127.0.0.1:8080     │      │ Proxy Listener: 8080      │            │
│  └───────────────────────────┘      └─────────────┬─────────────┘            │
└───────────────────────────────────────────────────┼──────────────────────────┘
                                                    │
                                             Bridged Network
                                                    │
                                                    ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                       Kali Linux VM (10.83.80.7)                             │
│                                                                              │
│  • Apache 2.4.66 Web Server                                                  │
│  • MariaDB 11.8.5 Database                                                   │
│  • DVWA (Damn Vulnerable Web Application)                                    │
│  • PHP 8.x                                                                   │
└──────────────────────────────────────────────────────────────────────────────┘
```

| Tool | Version | Purpose |
|:---|:---|:---|
| **Burp Suite CE** | 2026.1.3 | HTTP proxy, traffic interception, manual request analysis. |
| **Kali Linux** | 2026-W06 | Assessment platform hosting DVWA. |
| **DVWA** | Latest | Deliberately vulnerable web application (Target). |
| **VirtualBox** | Latest | Virtualisation and isolated lab network. |

---

## GRC Skills Demonstrated in This Project

1. **Risk Assessment Lifecycle:** Conducted a formal application risk assessment from initial information gathering to detailed remediation tracking.
2. **Compliance Frameworks:** Mapped identified vulnerabilities to specific ISO 27001 Annex A controls, NIST CSF functions, GDPR Article 32, and PCI DSS Requirement 6.5.
3. **Risk Quantification & Cost Analysis:** Utilized CVSS v3.0 and performed a Cost-Benefit Analysis (e.g., $800 fix vs. €20M GDPR fine) to justify security spending to a hypothetical CISO.
4. **Manual Testing over Automation:** Demonstrated the ability to manually test and chain vulnerabilities (XSS → Session Hijacking → CSRF) — an approach automated scanners routinely miss.
5. **Executive Communication:** Created an "Executive Dashboard" to translate complex injection flaws (SQLi, XSS) into measurable business risk (PII exfiltration).
6. **Residual Risk & Governance:** Formalized a "Residual Risk Assessment" to demonstrate understanding of risk acceptance protocols and management sign-off.
7. **SDLC Integration:** Recommended Shift-Left Security practices, including SAST integration and Security Champions, to prevent vulnerabilities at the source.

---

## Disclaimer & Ethics

> This assessment was conducted entirely in a **controlled, isolated VirtualBox lab environment** for educational purposes. DVWA is a deliberately vulnerable application created specifically for security training. It was deployed on a private VM with no internet exposure. No real-world systems, networks, production applications, or user data were involved. All activities were performed legally and ethically within a self-contained personal lab.

---

<div align="center">

*GRC2 · Burp Suite · OWASP WSTG · DVWA · CVSS v3.0 · ISO 27001 · NIST CSF*

*Web Application Risk Assessment · Business Impact Analysis · GDPR · PCI DSS*

</div>
