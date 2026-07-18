# 5. Risk Register & Business Impact Analysis

This register serves as the master document for tracking identified application weaknesses. Risks are quantified using **CVSS v3.0** and **Qualitative Business Impact (Low/Medium/High/Critical)**.

## Risk Scoring Context
*   **Asset Business Function:** Customer self-service portal (Handles PII, email addresses, and user credentials).
*   **Qualitative Risk Formula:** Risk = Likelihood of Exploitation × Business Impact.

## Risk Register Entries
| Priority | Vulnerability | CVSS | EPSS (Est.) | Likelihood | Business Impact | Risk Score | Recommended Owner |
|:---:|:---|:---:|:---:|:---|:---|:---:|:---|
| **P1** | **SQL Injection** | 9.8 | ~91% | Very High (Public-facing endpoint) | **Critical:** Full database extraction of PII & credentials. GDPR Breach. | Critical | Web App Developer |
| **P2** | **Brute Force & Credential Leakage** | 7.5 | ~43% | Very High (No rate limiting) | **High:** Account takeover. Credentials exposed in logs. | High | IAM / Security Team |
| **P2** | **Reflected Cross-Site Scripting (XSS)** | 7.3 | ~35% | High (Requires user interaction) | **High:** Session hijacking, credential theft, malware injection. | High | Web App Developer |
| **P3** | **Cross-Site Request Forgery (CSRF)** | 6.5 | ~22% | Medium (Requires social engineering) | **Medium:** Silent password changes leading to account takeover. | Medium | Web App Developer |

> **Note on EPSS:** While the Exact EPSS scores for these specific CVE patterns are not readily available for manual testing, the *Exploit Prediction Scoring System* statistically ranks SQL Injection and Brute Force as some of the highest-probability attack vectors in modern web attacks, validating their P1/P2 priority status.
