# 3. Assessment Scope & Technical Methodology

**Document Type:** Terms of Reference (ToR)
**Assessment Period:** February 18 – 19, 2026
**Assessment Owner:** [Your Name]

## 3.1 Purpose
To conduct a formal Web Application Risk Assessment. The objective is to identify technical vulnerabilities in the application logic, validate their exploitability, quantify business impact, and provide a prioritized remediation plan aligned with OWASP Top 10, ISO 27001, and NIST CSF.

## 3.2 In-Scope & Out-of-Scope Assets
| **Scope Element** | **Details** |
|:---|:---|
| **Application Name** | Damn Vulnerable Web Application (DVWA) - Customer Self-Service Portal |
| **Target URL** | `http://10.83.80.7/dvwa/` |
| **Target Infrastructure** | Kali Linux (Host), Apache 2.4.66, MariaDB 11.8.5, PHP 8.x |
| **Assessment Type** | Manual Application Security Review (Black-Box / Unauthenticated & Authenticated) |
| **Out-of-Scope** | The underlying operating system, cloud infrastructure, and external third-party APIs. |

## 3.3 Lab Architecture
The assessment was conducted on a virtualized bridged network to simulate a real-world web deployment.
*   **Assessment VM:** Kali Linux 2026-W06 (`10.83.80.7`)
*   **Proxy Tool:** Burp Suite Community Edition (v2026.1.3) running locally on the host, intercepting traffic routed via Firefox (`127.0.0.1:8080`).
*   **Target:** DVWA running locally on the Kali VM, accessible via the Bridged adapter.

## 3.4 Technical Methodology (OWASP WSTG & Manual Testing)
This assessment relies on **manual testing**, following the OWASP Web Security Testing Guide (WSTG) framework:

1.  **Information Gathering & Configuration:** Reviewed HTTP headers, cookie attributes, and server responses for security misconfigurations.
2.  **Input Validation Testing:** Tested all input vectors (`GET`, `POST`, URL parameters) for injection flaws. 
3.  **Authentication & Session Management:** Evaluated login mechanisms, password storage, and session tokens.
4.  **Access Control Testing:** Analyzed privilege escalation paths and Cross-Site Request Forgery vectors.
5.  **Traffic Analysis:** Intercepted all requests/responses via Burp Suite to analyze backend logic and data flows.

## 3.5 Risk Quantification & Prioritization
Once the technical findings were returned, they were analyzed using a blended scoring methodology to create a business-focused risk register:

1.  **CVSS v3.0 Base Score:** Provides the industry-standard impact/severity rating of the vulnerability itself.
2.  **Qualitative Exploit Likelihood:** High-level assessment based on OWASP threat modeling and the inherent exploitability of standard vulnerability classes.
3.  **Qualitative Business Impact:** Analyzed through the lens of operational disruption, regulatory non-compliance (GDPR, ISO 27001), and reputational damage.
4.  **Priority Matrix (P1 – P4):** Findings were bucketed into an actionable GRC remediation priority (P1 = Immediate, P4 = Scheduled).

## 3.6 Assessment Constraints & Limitations
*   **Community Edition Constraints:** Burp Suite CE is utilized. While it supports manual interception and analysis, it does not include the automated Active/Passive scanning features found in Burp Suite Professional.
*   **Time-Boxed Assessment:** This engagement represents a targeted point-in-time review. A comprehensive penetration test would require deeper fuzzing and automated scanning cycles over several days.

## 3.7 Deliverables
*   `docs/` - 11 formal audit-grade GRC artifacts (Executive Summary, Risk Register, Remediation Tracker, MITRE ATT&CK, etc.).
*   `screenshots/` - 23 annotated images of the lab setup and Burp Suite intercepts.
