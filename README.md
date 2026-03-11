# FUTURE_CS_01 — Vulnerability Assessment Report

## Overview

This repository contains a professional **Vulnerability Assessment Report** produced as part of the Future Interns Cyber Security internship programme (Task 01).  
The assessment was performed on a **deliberately vulnerable demo website** (`testphp.vulnweb.com`) that is maintained by Acunetix specifically for security testing and education purposes.  No production or privately-owned website was targeted.

---

## Website Tested

| Field | Detail |
|---|---|
| **Target URL** | `http://testphp.vulnweb.com` |
| **Type** | Intentionally vulnerable PHP demo site |
| **Owner / Maintained by** | Acunetix (publicly available for security testing) |
| **Test Date** | March 2026 |
| **Assessor** | Future Interns — Cyber Security Track |

---

## Scope

### In-Scope
- Public-facing pages (passive, read-only analysis)
- HTTP response header inspection
- Cookie attribute analysis
- Port & service exposure check (passive)
- Client-side information disclosure review

### Out-of-Scope (Explicitly Excluded)
- Login bypass or authentication attacks
- SQL injection exploitation
- Brute-force attacks
- Denial-of-Service (DoS)
- Any active exploitation

---

## Tools Used

| Tool | Purpose |
|---|---|
| **Nmap** | Port scanning & service enumeration |
| **OWASP ZAP (Passive Scan)** | Header checks, cookie analysis, passive vulnerability detection |
| **Browser DevTools** | Inspect response headers, cookies, and client-side scripts |
| **curl** | Manual HTTP header retrieval and verification |

---

## Repository Structure

```
FUTURE_CS_01/
├── README.md                          ← This file
├── report/
│   └── vulnerability_assessment_report.md   ← Full assessment report
└── evidence/
    ├── nmap_scan_output.txt           ← Raw Nmap scan results
    ├── headers_analysis.txt           ← HTTP response headers
    ├── owasp_zap_findings.md          ← OWASP ZAP passive scan findings
    └── cookie_analysis.txt            ← Cookie attribute review
```

---

## Key Findings Summary

| # | Vulnerability | Risk Level |
|---|---|---|
| 1 | Missing `Strict-Transport-Security` (HSTS) header | Medium |
| 2 | Missing `X-Frame-Options` header (Clickjacking risk) | Medium |
| 3 | Missing `X-Content-Type-Options` header | Low |
| 4 | Missing `Content-Security-Policy` (CSP) header | High |
| 5 | Session cookie missing `HttpOnly` flag | High |
| 6 | Session cookie missing `Secure` flag | High |
| 7 | Server version disclosure (`Apache` header) | Low |
| 8 | Open ports: 80 (HTTP) — no HTTPS redirect | Medium |
| 9 | PHP version disclosed in response headers | Low |
| 10 | Directory listing enabled | Low |

---

## Full Report

See [`report/vulnerability_assessment_report.md`](report/vulnerability_assessment_report.md) for the complete professional assessment, including detailed findings, risk classifications, business impact descriptions, and remediation steps.

---

## LinkedIn

> After completion, share your work on LinkedIn and tag [Future Interns](https://www.linkedin.com/company/future-interns).
