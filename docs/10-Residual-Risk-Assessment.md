# 10. Residual Risk Assessment

GRC is not about fixing every single vulnerability. It is about treating risk to align with the organization's **Risk Appetite**. Once we implement controls from the `04-Remediation-Tracker.md`, the risk doesn't vanish—it becomes **Residual Risk**.

This document outlines the transition from **Inherent Risk** (Risk before controls) to **Residual Risk** (Risk after controls), and obtains formal management buy-in for the remaining exposure.

## 10.1 Risk Scoring Methodology (Inherent vs. Residual)
*   **Inherent Risk:** The raw likelihood and impact of the vulnerability *before* any mitigation.
*   **Proposed Controls:** The specific action taken to reduce the risk.
*   **Residual Risk:** The remaining risk *after* the control is applied. It must be formally **Accepted** by the risk owner (CISO / CIO).

## 10.2 Residual Risk Register

| Vulnerability | Inherent Risk (Pre-Control) | Proposed GRC Control | Residual Risk (Post-Control) | Risk Owner Acceptance | Decision |
|:---|:---|:---|:---|:---|:---|
| **SQL Injection** | **Critical** (P1) <br>*(100% loss of PII data)* | 1. Implement PDO Prepared Statements.<br>2. Deploy a WAF (Web App Firewall) with SQLi rule sets.<br>3. Implement strict DB least-privilege (No `DROP` or `DELETE` for web user). | **Low** <br>*(Exploitation becomes virtually impossible via code; only 0-day WAF bypasses remain)* | CISO | **Accept** (after WAF & Code update) |
| **Brute Force & Auth** | **High** (P2) <br>*(100% chance of account compromise within weeks)* | 1. Implement Rate Limiting (5 attempts / 15 mins).<br>2. Enforce Account Lockout.<br>3. Migrate from `GET` to `POST` to hide credentials from logs.<br>4. Deploy MFA for Admin accounts. | **Low** <br>*(Attackers cannot use automated tools; physical/phishing attacks still remain)* | CISO | **Accept** (after MFA deployment) |
| **Reflected XSS** | **High** (P2) <br>*(Session hijacking leads to admin takeover)* | 1. Implement `htmlspecialchars()` output encoding.<br>2. Deploy a strict **Content Security Policy (CSP)** header blocking inline JS. | **Medium** <br>*(CSP can be bypassed by advanced attackers; yet the standard exploit is blocked)* | InfoSec Lead | **Transfer to DevSecOps** (Accept with monitoring) |
| **CSRF** | **Medium** (P3) <br>*(Silent admin password change)* | 1. Implement secure Anti-CSRF tokens for all `POST` operations.<br>2. Enforce `SameSite=Strict` cookie attribute. | **Low** <br>*(Social engineering remains a vector, but technical feasibility drops drastically)* | InfoSec Lead | **Accept** |

## 10.3 Executive Approval Matrix (Management Buy-In)

We recommend that the CISO formally accepts the *Low* and *Medium* residual risks documented above, as the proposed controls bring the application security posture into line with the company's **Conservative Risk Appetite** (as defined in `04-Assumed-Business-Context.md`).

> *"By accepting the residual risk associated with XSS and CSRF, we acknowledge that while a sophisticated, targeted 0-day attack may succeed, the organization's standard defensive controls (CSP, Tokens, WAF) reduce the likelihood to an acceptable level for a financial services platform."*
> *(CISO Sign-off required on the final audit report).*
