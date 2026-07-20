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
| **Tools Used** | Burp Suite CE (Manual Proxy), OWASP Top 10, Kali Linux, DVWA. |
| **Compliance Mapped** | ISO 27001 Annex A, NIST CSF, PCI DSS v4.0, GDPR. |
| **Key Deliverables** | Executive Dashboard, Assumed Business Context, Risk Register, Remediation Tracker, Residual Risk Assessment, Lessons Learned. |

---

## Repository Contents (Standard GRC Template)

This project utilizes a standardized **11-document GRC framework**. Browse the `/docs/` folder to view the complete assessment:

| # | Document Name | GRC Purpose |
|:---:|:---|:---|
| 01 | **Executive Summary** | Management-level overview of the engagement. |
| 02 | **Executive Dashboard** | KPI-driven metrics and quick-glance roadmap for senior leadership. |
| 03 | **Scope & Methodology** | Formal terms of reference and OWASP testing approach. |
| 04 | **Assumed Business Context** | Organizational profile, risk appetite, and asset sensitivity. |
| 05 | **Risk Register** | Detailed CVSS scoring, exploitability, and business impact analysis. |
| 06 | **Remediation Tracker** | Cost-benefit analysis, SDLC integration, and action item tracking. |
| 07 | **Compliance Gap Analysis** | Finding-to-control mapping (ISO 27001, NIST CSF, PCI DSS, GDPR). |
| 08 | **Asset Business Criticality** | Impact analysis based on the application's business function. |
| 09 | **MITRE ATT&CK Mapping** | Adversarial TTP mapping and kill-chain analysis. |
| 10 | **Residual Risk Assessment** | Management sign-off on accepted risk post-mitigation. |
| 11 | **Lessons Learned** | Post-engagement review, challenges, and growth insights. |

**Evidence Artifacts:**
*   `screenshots/` - 23 annotated screenshots documenting the lab setup, Burp Suite intercepts, and vulnerability exploitation.
*   `docs/` - 11 audit-grade `.md` files with formal GRC documentation.

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
1.  **Risk Assessment Lifecycle:** Performed a formal application risk assessment from initial information gathering to detailed remediation tracking.
2.  **Compliance Frameworks:** Mapped identified vulnerabilities to specific ISO 27001 Annex A controls, NIST CSF functions, GDPR Article 32, and PCI DSS Requirement 6.5.
3.  **Risk Quantification & Cost Analysis:** Utilized CVSS v3.0 and performed a Cost-Benefit Analysis (e.g., $800 fix vs. €20M GDPR fine) to justify security spending to a hypothetical CISO.
4.  **Executive Communication:** Created an "Executive Dashboard" to translate complex injection flaws (SQLi, XSS) into measurable business risk (PII exfiltration).
5.  **Residual Risk Management:** Formalized a "Residual Risk Assessment" to demonstrate understanding of risk acceptance protocols and management sign-off.

---

## Disclaimer

> This assessment was conducted entirely in a **controlled, isolated VirtualBox lab environment** for educational purposes. DVWA is a deliberately vulnerable application created specifically for security training. It was deployed on a private VM with no internet exposure. No real-world systems, networks, production applications, or user data were involved. All activities were performed legally and ethically within a self-contained personal lab.

---

<div align="center">

*GRC2 · Burp Suite · OWASP WSTG · DVWA · CVSS v3.0 · ISO 27001 · NIST CSF*

*Web Application Risk Assessment · Business Impact Analysis · GDPR · PCI DSS*

</div>
