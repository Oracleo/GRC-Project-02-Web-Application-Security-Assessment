# 8. Asset Business Criticality

In a professional GRC environment, a vulnerability against a test environment is vastly different from a vulnerability against a live production system. For the purposes of this risk engagement, we place the DVWA application into a realistic business context to accurately score the risk.

## 8.1 Asset Profile

| Asset Attribute | Assigned Context |
|:---|:---|
| **Application Name** | `CustomerHub - Self-Service Portal` |
| **Business Function** | Public-facing portal allowing customers to view order history, update personal profiles, and reset passwords. |
| **Data Sensitivity** | **High.** Hosts Personally Identifiable Information (PII) including full names, email addresses, home addresses, and hashed customer passwords. |
| **Regulatory Footprint** | Subject to **GDPR** for EU-based customers and local data privacy laws. |
| **Operational Criticality** | Business-critical. Portal downtime prevents customers from managing their accounts, leading to a 30% drop in self-service support efficiency. |

## 8.2 Impact Analysis Matrix

Because this asset handles customer PII and authentication data, the business impact of a successful compromise is severe:

| Threat Scenario | Operational Impact | Compliance Impact | Financial/Reputational Impact |
|:---|:---|:---|:---|
| **SQL Injection** | Full database dump of 500,000+ customer records. | Mandatory GDPR 72-hour breach notification to authorities. | €20M potential fine. Severe media coverage. |
| **Brute Force / Auth Failure** | Unauthorized account takeover of high-privilege users (Admins). | Violates PCI DSS 8.3 (Authentication controls). | Fraudulent actions performed on user accounts. |
| **XSS (Session Hijack)** | Attacker steals admin session cookies and compromises the admin panel. | Loss of customer trust and data integrity. | Litigation from customers whose data was stolen. |

## 8.3 Conclusion on Priority Scoring
The **SQL Injection** (CVSS 9.8) finding is escalated to a board-level *Critical P1*. While patching code is cheap, the *risk* is the exposure of 500,000 customer records. The priority matrix in the Risk Register (`05`) is directly driven by this high-value business context.
