# 3. Assessment Scope & Technical Methodology

*  **Document Type:** Terms of Reference (ToR)
*  **Assessment Period:** February 18 – 19, 2026
*  **Assessment Owner:** Niladri Biswas

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

> **Note on Environment:** Using a bridged network allows the web application to behave like a standard LAN-hosted web app, allowing the Burp Proxy to capture live HTTP/HTTPS traffic seamlessly. 

## 3.4 Technical Methodology (OWASP WSTG & Manual Testing)
This assessment relies on **manual testing**, following the OWASP Web Security Testing Guide (WSTG) framework:

1.  **Information Gathering & Configuration:** Reviewed HTTP headers, cookie attributes, and server responses for security misconfigurations.
2.  **Input Validation Testing:** Tested all input vectors (`GET`, `POST`, URL parameters) for injection flaws. 
3.  **Authentication & Session Management:** Evaluated login mechanisms, password storage, and session tokens.
4.  **Access Control Testing:** Analyzed privilege escalation paths and Cross-Site Request Forgery vectors.
5.  **Traffic Analysis:** Intercepted all requests/responses via Burp Suite to analyze backend logic and data flows.

## 3.5 Constraints & Limitations
*   **Community Edition Constraints:** Burp Suite CE is utilized. While it supports manual interception and analysis (essential for manual testing), it does not include the automated Active/Passive scanning features found in Burp Suite Professional (which requires a paid license).
*   **Time-Boxed Assessment:** This engagement represents a targeted point-in-time review. A comprehensive penetration test would require deeper fuzzing and automated scanning cycles over several days.
