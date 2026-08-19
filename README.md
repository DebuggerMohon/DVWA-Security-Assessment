# 🛡️ DVWA Vulnerability Assessment & Security Report

## 📌 Executive Summary
A comprehensive security assessment was conducted on **Damn Vulnerable Web Application (DVWA)** in a controlled laboratory environment. The primary objective was to identify, exploit, and remediate critical web application vulnerabilities based on the **OWASP Top 10** security risks.

---

## 🛠️ Tools & Methodology
- **Target App:** DVWA (Security Level: Low)
- **Scanning Tools:** Nmap, Nikto
- **Proxy & Testing:** Burp Suite, Web Browser Tools
- **Methodology:** OWASP Testing Guide

---

## 🔍 Identified Vulnerabilities & Proof of Concept (PoC)

### 1. Command Execution (OS Command Injection)
- **Severity:** High
- **Description:** The application fails to sanitize user inputs before passing them to system shell execution, allowing arbitrary command execution on the host machine.
- **Payload Used:** `192.168.187.129; whoami`
- **Impact:** System-level compromise and sensitive information exposure (`uid=33(www-data)` retrieved).
- **Proof of Concept:**
  ![Command Execution](screenshots/command_injection.png)
- **Remediation:** Use input sanitization and avoid system call functions like `exec()` or `system()`. Use parameter binding or built-in functions instead.

---

### 2. SQL Injection (SQLi)
- **Severity:** High
- **Description:** Unsanitized user inputs are concatenated directly into SQL queries, enabling authentication bypass and unauthorized database access.
- **Payload Used:** `' OR '1'='1`
- **Impact:** Full database dump and unauthorized user data retrieval.
- **Proof of Concept:**
  ![SQL Injection](screenshots/sqli.png)
- **Remediation:** Use Prepared Statements (Parameterized Queries) and ORM frameworks.

---

### 3. Stored Cross-Site Scripting (XSS)
- **Severity:** Medium
- **Description:** Malicious JavaScript payload stored in the database is executed automatically every time the page is loaded by a user.
- **Payload Used:** `<script>alert('XSS-Vulnerability')</script>`
- **Impact:** Session hijacking, credential theft, and malicious site redirection.
- **Proof of Concept:**
  ![Stored XSS](screenshots/xss.png)
- **Remediation:** Implement HTML entity encoding and strict input validation/sanitization.

---

## 📄 Conclusion & Recommendations
1. Implement Strict Input Sanitization across all web forms.
2. Utilize Prepared Statements for SQL database operations.
3. Apply Security Headers (e.g., CSP - Content Security Policy).

---
*Disclaimer: This security assessment was performed strictly for educational and authorization testing purposes in a isolated environment.*
