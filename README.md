# 🛡️ DVWA Vulnerability Assessment & Security Assessment Report

## 📌 Executive Summary
A comprehensive web application security assessment was performed on **Damn Vulnerable Web Application (DVWA)** in a controlled lab environment. The goal was to identify, exploit, and provide technical remediation for critical security flaws aligned with the **OWASP Top 10** vulnerabilities.

---

## 🛠️ Tools & Methodology
- **Target Application:** DVWA (Security Level: Low)
- **Scanners:** Nmap, Nikto
- **Interception Proxy:** Burp Suite
- **Testing Framework:** OWASP Web Security Testing Guide (WSTG)

---

## 🔍 Identified Vulnerabilities & Proof of Concept (PoC)

### 1. Command Execution (OS Command Injection)
- **Severity:** High (CVSS v3.1: 9.8)
- **Description:** The input field fails to sanitize OS command delimiters, allowing remote attackers to execute arbitrary system commands on the host server.
- **Payload:** `192.168.187.129; whoami`
- **Impact:** System privilege disclosure (`uid=33(www-data)`) and potential remote code execution (RCE).
- **Proof of Concept:**
  ![Command Execution](Screen_Shots/command_injection.png)
- **Remediation:** Avoid calling OS shell execution functions (e.g., `system()`, `exec()`). Implement strict input validation or use secure APIs.

---

### 2. SQL Injection (SQLi)
- **Severity:** Critical (CVSS v3.1: 9.8)
- **Description:** Dynamic SQL queries constructed with unsanitized user input allow authentication bypass and unauthorized database extraction.
- **Payload:** `' OR '1'='1`
- **Impact:** Complete exposure of database content, including user credentials and sensitive records.
- **Proof of Concept:**
  ![SQL Injection](Screen_Shots/sqli.png)
- **Remediation:** Implement Prepared Statements (Parameterized Queries) or Object-Relational Mapping (ORM) to separate data from execution logic.

---

### 3. Cross-Site Scripting (XSS)
- **Severity:** High (CVSS v3.1: 7.2)
- **Description:** Unfiltered client-side scripts are injected into the application and stored persistently, executing automatically in the context of other users' sessions.
- **Payload:** `<script>alert('XSS-Vulnerability')</script>`
- **Impact:** Session hijacking, cookie theft, and malicious client-side script execution.
- **Proof of Concept:**
  ![Cross-Site Scripting](Screen_Shots/xss.png)
- **Remediation:** Apply contextual HTML/JavaScript entity encoding before outputting user input to the DOM, and implement a strong Content Security Policy (CSP).

---

## 💡 Recommendations & Best Practices
1. **Context-Aware Input Validation:** Sanitize and validate all user inputs on the server side using allowlists.
2. **Parameterized Queries:** Use parameterized SQL interface across all database interactions to prevent SQLi.
3. **Output Encoding:** Encode output dynamically based on the rendering context (HTML, JS, CSS) to prevent XSS.

---
*Disclaimer: This report and test results are intended strictly for educational and portfolio purposes within an authorized laboratory environment.*
