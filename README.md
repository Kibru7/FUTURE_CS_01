Vulnerability Assessment — demo.testfire.net (2026-03-16)

•	Overview
This repository contains a security consulting-style vulnerability assessment of a public website using  read-only / passive techniques. The goal is to identify common security weaknesses, classify them in business-friendly risk levels, and provide practical remediation recommendations.

•	Website Tested
- Target: `https://demo.testfire.net/`
- Date tested:2026-03-16
- Observed IP (DNS): `65.61.137.117`

•	Scope & Ethics
This assessment followed strict ethical guidelines.

•	Allowed (performed)
- ✅ Public-facing pages only
- ✅ Passive scanning (OWASP ZAP Passive Scan)
- ✅ Security header and cookie checks
- ✅ Basic exposure/service validation (Nmap)
- ✅ Configuration analysis (read-only)

•	Not allowed (NOT performed)
- ❌ Exploitation
- ❌ Login bypass
- ❌ Brute force attacks
- ❌ Denial-of-Service (DoS)
- ❌ Any activity that could harm the website or its users

•	Tools Used
- Nmap — basic port & service exposure validation  
- OWASP ZAP (Passive Scan only) — passive vulnerability identification  
- curl / Browser DevTools — response header and cookie attribute checks  
- dig — DNS record inspection  

•	Repository Contents
- `report/`
  - Final PDF report exported from Canva
- `evidence/screenshots/`
  - Screenshots of OWASP ZAP passive alerts (8 alert types)
- `evidence/tool-outputs/`
  
•	How to Use This Repo
1. Open the PDF in `report/` for the business-friendly audit.
2. Review `evidence/` for supporting screenshots and raw tool outputs.

•	Disclaimer
This project is for educational purposes and focuses on security auditing and reporting, not hacking. All testing was performed using passive, non-destructive techniques against a publicly accessible demo site.
