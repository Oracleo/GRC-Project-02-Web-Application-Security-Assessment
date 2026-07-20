# 5. Risk Register

This register serves as the master document for tracking identified application weaknesses. Risks are quantified using **CVSS v3.0**, **CVSS Vector Strings**, and **Qualitative Business Impact (Low/Medium/High/Critical)**.

## Risk Scoring Context
*   **Asset Business Function:** Customer self-service portal (Handles PII, email addresses, and user credentials).
*   **Qualitative Risk Formula:** Risk = Likelihood of Exploitation × Business Impact.

## Risk Register Entries

| Priority | Finding | CVSS | CVSS Vector | Exploit Likelihood (Qualitative) | Business Impact | Risk Score | Recommended Owner |
|:---:|:---|:---:|:---|:---|:---|:---:|:---|
| **P1** | **SQL Injection** | 9.8 | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` | Very High (Public-facing endpoint) | **Critical:** Full database extraction of PII & credentials. GDPR Breach. | Critical | Web App Developer |
| **P2** | **Brute Force & Credential Leakage** | 7.5 | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N` | Very High (No rate limiting) | **High:** Account takeover. Credentials exposed in logs. | High | IAM / Security Team |
| **P2** | **Reflected Cross-Site Scripting (XSS)** | 7.3 | `AV:N/AC:H/PR:N/UI:R/S:U/C:H/I:H/A:H` | High (Requires user interaction) | **High:** Session hijacking, credential theft, malware injection. | High | Web App Developer |
| **P3** | **Cross-Site Request Forgery (CSRF)** | 6.5 | `AV:N/AC:L/PR:N/UI:R/S:U/C:L/I:L/A:N` | Medium (Requires social engineering) | **Medium:** Silent password changes leading to account takeover. | Medium | Web App Developer |

> **Note on Likelihood:** While EPSS (Exploit Prediction Scoring System) is an excellent metric for published CVEs, it does not apply to bespoke application logic vulnerabilities (which lack a CVE ID). Therefore, a **Qualitative Exploit Likelihood** is utilized to correctly model the threat environment for this custom web application.
