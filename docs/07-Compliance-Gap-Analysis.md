# 7. Compliance Gap Analysis (ISO, NIST, PCI DSS, GDPR)

This document maps the identified technical vulnerabilities to specific regulatory frameworks, demonstrating the direct governance impact of the application flaws.

## ISO 27001:2022 Annex A Mappings
| Control ID | Control Name | Vulnerability Evidence | Compliance Status |
|:---:|:---|:---|:---:|
| **A.8.28** | Secure Coding | SQLi and XSS directly indicate a failure to follow secure coding practices during development. | 🔴 **Non-Compliant** |
| **A.8.29** | Security Testing in Development | These vulnerabilities exist in production, indicating no pre-release security testing occurred. | 🔴 **Non-Compliant** |
| **A.8.26** | Application Security Requirements | CSRF vulnerability indicates missing security requirements during the design phase. | 🟡 **Control Gap** |
| **A.8.5** | Secure Authentication | Brute Force vulnerability demonstrates weak authentication requirements. | 🔴 **Non-Compliant** |
| **A.5.17** | Authentication Information | Passwords transmitted in GET parameters are vulnerable to log leakage. | 🔴 **Non-Compliant** |

## NIST Cybersecurity Framework (CSF) Mappings
| NIST Function | NIST Category | Vulnerability Evidence |
|:---|:---|:---|
| **PROTECT (PR)** | PR.IP-2 (System Development Lifecycle) | Insecure coding (SQLi, XSS) proves security was not embedded in the SDLC. |
| **PROTECT (PR)** | PR.AC-7 (Authentication) | The Brute Force vulnerability directly violates PR.AC-7. |
| **IDENTIFY (ID)** | ID.RA-1 (Asset Vulnerabilities) | Assessment performed; risk register produced to identify these vulnerabilities. |

## PCI DSS v4.0 (Payment Card Industry) Mappings
*Application is simulated as a customer portal, but PCI DSS mappings apply to any organization securing data. If credit card data were processed here:*
*   **Requirement 6.5:** "Address common security vulnerabilities in software development."
    *   **6.5.1:** Injection flaws (SQLi, XSS) must be addressed.
    *   **6.5.10:** Cross-Site Request Forgery (CSRF) must be addressed.
    *   **Result:** Immediate Audit Failure.

## GDPR (General Data Protection Regulation) Breach Risks
*   **Article 32 (Security of Processing):** SQLi enables unauthorized access to PII (names, emails). This is a failure to implement appropriate technical measures.
*   **Article 33 (Notification):** Exploitation of SQLi resulting in PII exfiltration triggers a mandatory 72-hour notification requirement to the ICO/Supervisory Authority.
*   **Article 5(1)(f) (Integrity and Confidentiality):** The Brute Force and XSS vulnerabilities fail to protect personal data from unauthorized processing.

**Compliance Conclusion:** The application is currently non-compliant with ISO 27001, violates PCI DSS secure coding requirements, and poses a direct threat to GDPR compliance if the PII data is compromised.
