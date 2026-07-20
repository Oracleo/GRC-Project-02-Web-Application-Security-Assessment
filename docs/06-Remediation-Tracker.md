# 6. Remediation Tracker

This artifact tracks the remediation plan with a **Cost-Benefit Analysis** to justify developer sprint time, and integrates actions into the **Software Development Lifecycle (SDLC)** to prevent recurrence.

## Cost-Benefit Context
*   **Cost of Inaction (Breach):** GDPR Article 33 requires notification within 72 hours. Data breach fines can reach up to **€20 Million** or 4% of global annual turnover. 
*   **Cost of Remediation:** Developer hours to patch vulnerable code blocks ($100 - $200/hr).

| Priority | Finding | Remediation Action | Assigned To | Due Date | Remediation Cost (Effort) | Cost of Inaction | Status |
|:---:|:---|:---|:---|:---:|:---|:---|:---|
| **P1** | **SQL Injection** | 1. Rewrite DB queries using PHP PDO Prepared Statements (`$stmt->bindParam`).<br>2. Apply output encoding to all database results. | Lead Developer | **Immediate** | **~$800** (4 hours dev time) | **> €20 Million** | Not Started |
| **P2** | **Brute Force / Auth Weakness** | 1. Migrate `GET` authentication to `POST`.<br>2. Implement Rate Limiting (max 5 attempts / 15 mins).<br>3. Deploy Account Lockout (5 failures).<br>4. Enforce HTTPS/SSL for all requests. | Security Engineer | 7 Days | **~$500** (Setup + Testing) | **~$500,000** (IR + Legal Fees) | In Progress |
| **P2** | **Reflected XSS** | 1. Apply `htmlspecialchars($input, ENT_QUOTES, 'UTF-8')` to all user inputs.<br>2. Deploy Strict Content Security Policy (CSP) header to prevent unauthorized JS execution. | Developer | 7 Days | **~$400** (2 hours dev time) | **~$1M** (Reputation + Litigation) | Not Started |
| **P3** | **CSRF** | 1. Generate and validate unique Anti-CSRF tokens per session for all `POST` requests.<br>2. Implement `SameSite=Strict` cookie attribute. | Developer | 30 Days | **~$300** (Framework integration) | **~$100,000** (Account takeover cleanup) | Not Started |

## SDLC (Software Development Lifecycle) Control Recommendations
*   **Shift Left Security:** Mandate that all code passes a **Static Application Security Testing (SAST)** tool (e.g., SonarQube, Semgrep) before a Pull Request can be merged. SQLi and XSS are highly detectable by SAST tools.
*   **Framework Adoption:** Migrate development to modern frameworks (e.g., Laravel, Symfony, Django) which provide built-in, default protections against SQLi and CSRF.
*   **Security Champions:** Assign a lead developer to be the "AppSec Champion" responsible for reviewing peer code for OWASP Top 10 flaws.
