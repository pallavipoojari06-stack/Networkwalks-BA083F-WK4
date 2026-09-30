# 🔐 Web Penetration Testing & Vulnerability Assessment

## 📌 Overview

This project was completed as part of a **cybersecurity penetration testing training project**.

The main goal was to identify common security weaknesses in a web application and understand how these vulnerabilities could affect the confidentiality and security of sensitive information.

The assessment was performed in an **authorized and controlled training environment**.

---

## 🎯 Objectives

* Perform basic web reconnaissance
* Identify open ports and running services
* Discover hidden web directories
* Test web application authentication
* Identify SQL Injection vulnerabilities
* Analyze exposed files and directories
* Test the strength of encrypted PDF documents
* Examine document metadata
* Provide security recommendations

---

## 🛠️ Tools Used

| Tool             | Purpose                       |
| ---------------- | ----------------------------- |
| `whois`          | Domain information            |
| `nslookup`       | DNS information               |
| `whatweb`        | Web technology identification |
| `curl`           | HTTP header inspection        |
| `wafw00f`        | WAF detection                 |
| `dnsrecon`       | DNS reconnaissance            |
| `Nmap`           | Port and service scanning     |
| `Gobuster`       | Directory enumeration         |
| `qpdf`           | PDF analysis and decryption   |
| `ExifTool`       | Metadata analysis             |
| Password Cracker | Authorized password testing   |

---

## 🔎 Methodology

### 1. Reconnaissance

The first step was gathering basic information about the target.

Activities included:

* Domain information gathering
* DNS lookup
* Web technology identification
* WAF detection
* HTTP header analysis

---

### 2. Network Scanning

Nmap was used to identify accessible ports and services.

The assessment identified services such as:

* FTP
* SMTP
* HTTP/HTTPS
* POP3/IMAP

This helped understand the external attack surface.

---

### 3. Directory Enumeration

Gobuster was used to discover directories that were not directly visible from the website.

Example discovered paths included:

```text
/cgi-bin
/staff
/mailman
/pipermail
/old
/webmail
```

The `/old` directory was identified as particularly important because it exposed an old database backup.

---

### 4. SQL Injection Testing

The patient login functionality was tested for input validation problems.

The testing showed that the application:

* Revealed whether a username existed
* Returned detailed database errors
* Was vulnerable to SQL Injection
* Allowed authentication to be bypassed in the training environment

This demonstrated the importance of **parameterized queries and proper input validation**.

---

### 5. PDF Security Testing

Password-protected PDF reports were also tested in the authorized environment.

The testing showed that some documents used weak passwords that could be recovered using dictionary-based password testing.

This demonstrated why sensitive documents should use:

* Strong unique passwords
* Modern encryption
* Proper key management

---

### 6. Metadata Analysis

After authorized decryption of the test documents, ExifTool was used to inspect metadata.

Metadata analysis helped identify information that could reveal details about how files were handled internally.

---

## ⚠️ Main Findings

### 🔴 SQL Injection

**Issue:**
The patient login functionality did not properly sanitize user input.

**Impact:**
An attacker could potentially bypass authentication and access restricted functionality.

**Recommendation:**

Use prepared statements:

```php
$stmt = $conn->prepare(
    "SELECT id, password_hash FROM patients WHERE username = ?"
);
$stmt->bind_param("s", $username);
$stmt->execute();
```

---

### 🔴 Exposed Backup Directory

**Issue:**
An old web directory contained a database backup.

**Impact:**
Sensitive business information could potentially be exposed to unauthorized users.

**Recommendation:**

* Remove database backups from the web root
* Store backups outside publicly accessible directories
* Disable directory listing
* Apply proper access controls

Example:

```apache
Options -Indexes
```

---

### 🟠 Username Enumeration

**Issue:**
Different error messages were returned for valid and invalid usernames.

For example:

```text
Username not found
Incorrect password
```

**Recommendation:**

Use a generic error message:

```text
Invalid username or password.
```

This makes username enumeration more difficult.

---

### 🟠 Weak PDF Passwords

**Issue:**
Some password-protected documents used weak passwords.

**Recommendation:**

* Use strong random passwords
* Avoid default passwords
* Use modern encryption standards
* Apply proper password management

---

## 🛡️ Security Recommendations

1. Use **prepared statements** to prevent SQL Injection.
2. Validate and sanitize user input.
3. Never store database backups inside the public web directory.
4. Disable directory listing.
5. Use generic authentication error messages.
6. Use strong passwords for sensitive documents.
7. Regularly review file and document metadata.
8. Keep web applications and server software updated.
9. Perform regular vulnerability assessments.
10. Protect sensitive healthcare and business information using appropriate access controls.

---

## 📚 What I Learned

Through this project, I gained practical experience with:

* Web reconnaissance
* Network scanning
* Directory enumeration
* SQL Injection concepts
* Authentication security
* Password security
* PDF analysis
* Metadata analysis
* Vulnerability reporting
* Security remediation

---

## ⚠️ Disclaimer

This project was performed as part of an **authorized cybersecurity training/lab environment**.

All security testing should only be performed against systems for which you have explicit permission.

---

## 👩‍💻 Author

**Pallavi Poojari**

Cybersecurity Student | Networking & Cybersecurity Enthusiast

GitHub: **pallavipoojari06-stack**
