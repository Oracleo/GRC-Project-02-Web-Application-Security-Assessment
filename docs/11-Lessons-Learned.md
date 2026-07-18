# 11. Lessons Learned & Continuous Improvement

Every GRC engagement should conclude with an After-Action Review (AAR). Documenting "Lessons Learned" demonstrates self-awareness, a commitment to continuous improvement, and an understanding that security is an iterative process.

## 11.1 What Went Well (Successes)
*   **Manual Testing Over Automated Scanning:** By manually testing via Burp Suite (rather than just running a scanner), I was able to *chain* vulnerabilities. I understood that an XSS could be used to steal a session cookie, which could then be used to execute a CSRF attack—a true pentesting approach that automated scanners miss.
*   **Live Traffic Visibility:** Configuring Firefox as a Burp Proxy and intercepting live traffic provided an unparalleled view of how HTTP headers, cookies, and URL parameters interact with the backend application logic.
*   **Frameworks Execution:** Successfully mapping Burp findings to **ISO 27001, PCI DSS, and MITRE ATT&CK** proved that I understand the business and adversary impacts, not just the technical bug.

## 11.2 What Could Be Improved (Challenges)
*   **Burp Suite CE Limitations:** Burp Suite Community Edition lacks the Active/Passive automated scanning engines found in Burp Professional. This meant I had to manually test every input vector. While this improves testing depth, it limits scale. I mitigated this by using OWASP WSTG as my guiding manual checklist.
*   **Time Constraints:** Manual testing is incredibly time-consuming. If this were a production environment, testing a large application with thousands of endpoints would require several weeks.
*   **Scope Boundaries:** This engagement was limited to a single DVWA instance. Testing large, modern Single Page Applications (SPAs) with APIs (REST/GraphQL) requires a shift to different tools (e.g., Postman, OWASP ZAP).

## 11.3 Key Risk Management Insights
*   **CVSS is not the only factor:** The CSRF vulnerability had a CVSS of 6.5 (Medium). However, because the application processes high-value customer PII, I upgraded this to a **P3 (30-day)** priority. *Always adjust technical scores based on business context.*
*   **Remediation Cost justifies the priority:** Patching the SQL injection costs around $800 in developer time. A data breach costs millions. This sharp contrast makes it incredibly easy to build a business case for the CISO.

## 11.4 Recommendations for Future Engagements
1.  **Introduce Automated SAST:** While manual manual pentesting is crucial, a Static Application Security Testing (SAST) tool integrated into the CI/CD pipeline would have caught the SQLi and XSS before the code was deployed to the staging environment (Shift-Left Security).
2.  **Include an Authenticated Phase:** If production credentials were provided, I could have tested for Horizontal/Vertical Privilege Escalation—currently a gap in this unauthenticated assessment.
3.  **Add a Penetration Testing Roadmap:** Future reports should include a "Pentesting Roadmap" that outlines the specific endpoints and business logic flows tested, allowing auditors to verify coverage.

> **Final GRC Takeaway:** Vulnerabilities will always exist. The job of a GRC analyst is to identify them, demonstrate their business risk, propose cost-effective controls, and formally track their resolution. This project successfully demonstrated that entire lifecycle.
