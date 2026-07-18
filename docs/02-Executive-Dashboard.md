# 2. Executive Dashboard

**Assessment Date:** February 19, 2026
**Assessment Type:** Manual Web Application Security Assessment
**Target Application:** `CustomerHub` Self-Service Portal (Simulated)

---

## Key Performance Indicators (KPIs) at a Glance

| Metric | Value | Status |
|:---|:---:|:---:|
| **Total Vulnerabilities** | 4 | ⚠️ **Moderate Risk** |
| **Critical (P1)** | 1 (SQL Injection) | 🔴 **Immediate Attention** |
| **High (P2)** | 2 (Brute Force, XSS) | 🟠 **Urgent Action Required** |
| **Medium (P3)** | 1 (CSRF) | 🟡 **Scheduled Action** |
| **Asset Criticality** | High (PII Data) | 🔴 **High Impact Potential** |
| **Average CVSS Score** | 7.8 (High) | ⚠️ **Risk Exposure** |
| **Estimated EPSS (90-Day)** | ~54% (Average Exploit Probability) | ⚠️ **High Active Threat Level** |

---

## Compliance Posture Assessment

| Framework | Status | Key Findings Impacting Compliance |
|:---|:---:|:---|
| **ISO 27001:2022** | ❌ **Non-Compliant** | A.8.28 (Secure Coding) violated by SQLi & XSS. |
| **PCI DSS v4.0** | ❌ **Non-Compliant** | Requirement 6.5 (Injection flaws & CSRF controls) failed. |
| **GDPR (EU)** | ⚠️ **High Breach Risk** | SQLi facilitates unauthorized PII access (Violation of Art. 32). |
| **OWASP Top 10 (2021)** | ❌ **Critical Failures** | A03:2021 (Injection) & A07:2021 (Auth Failures) identified. |

---

## Remediation Roadmap (Priority Funnel)

| Priority | Finding | Target Status | Owner | Due Date |
|:---:|:---|:---:|:---:|:---:|
| **P1** | **SQL Injection** | `Rewrite DB queries using PDO` | Lead Developer | **Immediate** |
| **P2** | **Brute Force & Auth** | `Enforce Rate Limiting & MFA` | DevOps / IAM | **7 Days** |
| **P2** | **Reflected XSS** | `Implement Output Encoding & CSP` | Frontend Dev | **7 Days** |
| **P3** | **CSRF** | `Implement Anti-CSRF Tokens` | Backend Dev | **30 Days** |

> **Executive Bottom Line:** The application is currently in a critical state regarding data privacy. Immediate funding of roughly $1,500-$2,000 in developer hours is required to fix the P1 & P2 flaws. Failure to do so exposes the organization to **€20M+ GDPR fines and severe reputational damage**.
