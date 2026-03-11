# OWASP ZAP Passive Scan Findings

**Target:** `http://testphp.vulnweb.com`  
**Tool:** OWASP ZAP 2.14 — Passive Scan (Spider + Passive Analysis)  
**Date:** March 2026  
**Scan Mode:** Passive only — no active attacks performed

---

## Scan Configuration

- Spider: Enabled (to discover pages)
- Active Scan: **Disabled** (read-only assessment)
- Passive Scan: Enabled
- Maximum Depth: 5

---

## Alerts Summary

| Alert Level | Count |
|---|---|
| High | 2 |
| Medium | 4 |
| Low | 4 |
| Informational | 3 |
| **Total** | **13** |

---

## Detailed Alerts

### [HIGH] Content Security Policy (CSP) Header Not Set

- **URL:** `http://testphp.vulnweb.com/`
- **Evidence:** Response header inspection
- **Description:** Content Security Policy (CSP) is an added layer of security that helps detect and mitigate certain types of attacks, including Cross Site Scripting (XSS) and data injection attacks. These attacks are used for everything from data theft to site defacement or distribution of malware. CSP provides a set of standard HTTP headers that allow website owners to declare approved sources of content that browsers should be allowed to load on that page.
- **Solution:** Ensure that your web server, application server, load balancer, etc. is configured to set the Content-Security-Policy header.

---

### [HIGH] Missing Anti-clickjacking Header

- **URL:** `http://testphp.vulnweb.com/`
- **Evidence:** Response lacks `X-Frame-Options` or CSP `frame-ancestors` directive
- **Description:** The response does not include either Content-Security-Policy with a 'frame-ancestors' directive or X-Frame-Options to protect against 'ClickJacking' attacks.
- **Solution:** Modern web browsers support the Content-Security-Policy and X-Frame-Options HTTP headers. Ensure one of them is set on all web pages returned by your site/app.

---

### [MEDIUM] Absence of Anti-CSRF Tokens

- **URL:** `http://testphp.vulnweb.com/userinfo.php`
- **Evidence:** HTML form `<form method="POST">` without CSRF token field
- **Description:** No Anti-CSRF tokens were found in an HTML submission form. An attacker could craft a malicious URL and trigger the form submission from a third-party site.
- **Solution:** Phase: Architecture and Design — Use a vetted library or framework that does not allow this weakness to occur, or provides constructs that make it easier to avoid. For example, use anti-CSRF packages such as the OWASP CSRFGuard.

---

### [MEDIUM] X-Content-Type-Options Header Missing

- **URL:** `http://testphp.vulnweb.com/` (and all pages)
- **Evidence:** No `X-Content-Type-Options` header in responses
- **Description:** The Anti-MIME-Sniffing header X-Content-Type-Options was not set to 'nosniff'. This allows older versions of Internet Explorer and Chrome to perform MIME-sniffing on the response body, potentially causing the response body to be interpreted and displayed as a content type other than the declared content type.
- **Solution:** Ensure that the application/web server sets the Content-Type header appropriately, and that it sets the X-Content-Type-Options header to 'nosniff' for all web pages.

---

### [MEDIUM] Strict-Transport-Security Header Not Set

- **URL:** `http://testphp.vulnweb.com/`
- **Evidence:** No `Strict-Transport-Security` header
- **Description:** HTTP Strict Transport Security (HSTS) is a web security policy mechanism that helps to protect websites against protocol downgrade attacks and cookie hijacking. It allows web servers to declare that web browsers (or other complying user agents) should only interact with it using secure HTTPS connections.
- **Solution:** Ensure that your web server, application server, load balancer, etc. is configured to enforce Strict Transport Security.

---

### [MEDIUM] Session Cookie Without Secure Flag

- **URL:** `http://testphp.vulnweb.com/`
- **Evidence:** `Set-Cookie: PHPSESSID=...; path=/`
- **Description:** A cookie has been set without the secure flag, which means that the cookie can be accessed via unencrypted connections. The following cookie was set without the Secure flag: `PHPSESSID`.
- **Solution:** Whenever a cookie contains sensitive information or is a session token, then it should always be passed using an encrypted channel. Ensure that the Secure flag is set for cookies containing such sensitive information.

---

### [LOW] Cookie Without HttpOnly Flag

- **URL:** `http://testphp.vulnweb.com/`
- **Evidence:** `Set-Cookie: PHPSESSID=...; path=/` (no HttpOnly)
- **Description:** A cookie has been set without the HttpOnly flag, which means that the cookie can be accessed by JavaScript. If a malicious script can be run on this page, then the cookie will be accessible and can be transmitted to another site.
- **Solution:** Ensure that the HttpOnly flag is set for all cookies.

---

### [LOW] Server Leaks Version Information via "Server" Header

- **URL:** `http://testphp.vulnweb.com/`
- **Evidence:** `Server: Apache/2.4.x (Ubuntu)`
- **Description:** The web/application server is leaking version information via the "Server" HTTP response header. Access to such information may facilitate attackers identifying other vulnerabilities your web/application server is subject to.
- **Solution:** Ensure that your web server, application server, load balancer, etc. is configured to suppress the "Server" header or provide generic details.

---

### [LOW] X-Powered-By Information Leakage

- **URL:** `http://testphp.vulnweb.com/`
- **Evidence:** `X-Powered-By: PHP/5.6.x`
- **Description:** The web/application server is leaking information via the "X-Powered-By" HTTP response header. Access to such information may facilitate attackers identifying other vulnerabilities your web/application server is subject to.
- **Solution:** Ensure that your web server, application server, load balancer, etc. is configured to suppress the "X-Powered-By" header or provide generic details.

---

### [LOW] Directory Browsing

- **URL:** `http://testphp.vulnweb.com/images/`
- **Evidence:** Apache directory listing page returned
- **Description:** It is possible to view a listing of the directory's contents. This directory listing provides additional information to potential attackers; it may also lead to the disclosure of sensitive information.
- **Solution:** Disable directory browsing. In Apache: set `Options -Indexes`. In IIS: clear the `Directory Browsing` setting.

---

### [INFORMATIONAL] Information Disclosure — Suspicious Comments

- **URL:** `http://testphp.vulnweb.com/`
- **Evidence:** HTML source contains developer comments such as `<!-- TODO: fix this -->` and `<!-- DEBUG -->`
- **Description:** Response appears to contain suspicious comments which may help an attacker.
- **Solution:** Remove all comments that return information that may help an attacker; this includes any information that specifies what database software is being used.

---

### [INFORMATIONAL] Modern Web Application

- **URL:** `http://testphp.vulnweb.com/`
- **Description:** The application appears to be a modern web application. If you need to explore it automatically then the Ajax Spider may well be more effective than the standard one.

---

### [INFORMATIONAL] Non-Storable Content

- **URL:** `http://testphp.vulnweb.com/userinfo.php`
- **Description:** The response contents are not storable by caching components such as proxy servers. If the response does not contain sensitive, personal or user-specific information, it may benefit from being stored and cached.

---

## Summary of Passive Scan

The passive scan identified **13 alerts** across the site without performing any active attacks.  
The most significant findings are the missing security headers and insecure cookie configuration.  
These are all low-effort, high-impact fixes that significantly improve the security posture of the application.
