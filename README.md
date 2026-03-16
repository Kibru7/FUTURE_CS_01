# FUTURE_CS_01 — Web Vulnerability Assessment Report

![Report Version](https://img.shields.io/badge/Report%20Version-2.0-blue)
![Findings](https://img.shields.io/badge/Findings-13-red)
![Risk: Critical](https://img.shields.io/badge/Critical-1-critical)
![Risk: High](https://img.shields.io/badge/High-4-orange)
![Risk: Medium](https://img.shields.io/badge/Medium-5-yellow)
![Risk: Low](https://img.shields.io/badge/Low-3-informational)
![Assessment Type](https://img.shields.io/badge/Assessment%20Type-Passive%20%2F%20Read--Only-green)
![OWASP WSTG](https://img.shields.io/badge/Methodology-OWASP%20WSTG%20v4.2-blueviolet)

## Overview

This repository contains a professional **Web Vulnerability Assessment Report** produced as part of the Future Interns Cyber Security internship programme (Task 01).

The assessment was performed on **`testphp.vulnweb.com`** — a deliberately vulnerable PHP demo application maintained by Acunetix specifically for security testing education. No production or privately-owned website was targeted.

---

## Website Tested

| Field | Detail |
|---|---|
| **Target URL** | `http://testphp.vulnweb.com` |
| **Target IP** | 44.228.249.3 |
| **Type** | Intentionally vulnerable PHP demo application |
| **Owner / Maintained by** | Acunetix (publicly available for security training) |
| **Technology Stack** | Apache HTTP Server, PHP 5.6 (EOL) |
| **Assessment Date** | March 2026 |
| **Assessor** | Future Interns — Cyber Security Track |

---

## Scope

### ✅ In-Scope (Allowed)
- Public-facing pages (passive, read-only analysis only)
- HTTP response header inspection
- Cookie attribute analysis
- Port & service enumeration (passive Nmap)
- Client-side HTML/JS source review (DevTools)
- Passive vulnerability scanning (OWASP ZAP passive mode)
- Form structure observation (no submission)

### ❌ Out-of-Scope (Explicitly Prohibited)
- Login bypass or authentication attacks
- SQL injection exploitation
- Cross-site scripting payload injection
- Brute-force attacks
- Denial-of-Service (DoS)
- Any form of active exploitation

---

## Tools Used

| Tool | Version | Purpose |
|---|---|---|
| **Nmap** | 7.94 | Port scanning & service enumeration |
| **OWASP ZAP** | 2.14 | Passive vulnerability scanning |
| **Browser DevTools** | Chrome 122 / Firefox 123 | Headers, cookies, source inspection |
| **curl** | 8.x | Manual HTTP header retrieval |

---

## Repository Structure

```
FUTURE_CS_01/
├── README.md                               ← This file
├── report/
│   └── vulnerability_assessment_report.md  ← Full assessment report (v2.0)
├── evidence/
│   ├── nmap_scan_output.txt                ← Nmap port scan results
│   ├── headers_analysis.txt                ← HTTP response header audit
│   ├── cookie_analysis.txt                 ← Cookie attribute review
│   ├── owasp_zap_findings.md               ← OWASP ZAP passive scan findings
│   ├── form_analysis.txt                   ← Form security analysis (CSRF, inputs)
│   └── source_code_review.txt              ← Client-side source code observations
├── methodology/
│   └── test_plan.md                        ← OWASP WSTG-aligned test plan
└── remediation/
    └── quick_reference_checklist.md        ← One-page developer hardening checklist
```

---

## Key Findings Summary

| # | ID | Vulnerability | CVSS | Risk |
|---|---|---|---|---|
| 1 | F-01 | No HTTPS — unencrypted traffic | 9.1 | 🔴 Critical |
| 2 | F-02 | Missing Content Security Policy (CSP) | 8.1 | 🟠 High |
| 3 | F-03 | Session cookie missing HttpOnly, Secure, SameSite | 8.0 | 🟠 High |
| 4 | F-04 | SQL Injection indicators (passive observation) | 8.6 | 🟠 High |
| 5 | F-05 | Reflected XSS indicators (passive observation) | 7.2 | 🟠 High |
| 6 | F-06 | No anti-CSRF tokens in forms | 6.5 | 🟡 Medium |
| 7 | F-07 | Missing X-Frame-Options (Clickjacking) | 6.1 | 🟡 Medium |
| 8 | F-08 | Missing HSTS header | 5.9 | 🟡 Medium |
| 9 | F-09 | Missing X-Content-Type-Options | 5.3 | 🟡 Medium |
| 10 | F-10 | Missing Referrer-Policy header | 4.3 | 🟡 Medium |
| 11 | F-11 | PHP 5.6 (EOL) version disclosed | 3.7 | 🔵 Low |
| 12 | F-12 | Apache server version disclosed | 3.1 | 🔵 Low |
| 13 | F-13 | Directory listing enabled | 2.6 | 🔵 Low |

---

## Quick Security Grade

```
Overall Security Grade:  F
─────────────────────────────────────
Transport Security:      F  (no HTTPS)
Security Headers:        F  (0 / 6 present)
Cookie Security:         F  (no flags set)
Input Handling:          F  (SQLi + XSS indicators)
─────────────────────────────────────
```

---

## Attack Chain Highlight

The report documents two complete **attack chains** showing how these findings combine:

1. **Network eavesdrop → account takeover** (requires only shared Wi-Fi access)
2. **Reflected XSS → session hijack → CSRF account change** (medium skill)

See [Section 8 of the report](report/vulnerability_assessment_report.md#8-attack-chain-analysis) for the step-by-step breakdowns.

---

## Documents

| Document | Description |
|---|---|
| [📄 Full Report](report/vulnerability_assessment_report.md) | Complete professional assessment with CVSS scores, CWE IDs, business impact, and remediation |
| [🗺️ Test Plan](methodology/test_plan.md) | OWASP WSTG v4.2–aligned test methodology |
| [✅ Hardening Checklist](remediation/quick_reference_checklist.md) | One-page quick-reference fix list for developers |

---

## LinkedIn

After completion, share your work on LinkedIn and tag [Future Interns](https://www.linkedin.com/company/future-interns).
