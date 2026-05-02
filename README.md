# FUTURE_CS_03 — API Security Risk Analysis Report
## Future Interns | Cyber Security Track | Task 3

![Cyber Security](https://img.shields.io/badge/Cyber%20Security-Internship-blue)
![API Security](https://img.shields.io/badge/Domain-API%20Security-red)
![OWASP](https://img.shields.io/badge/Methodology-OWASP%20API%20Top%2010-orange)
![Status](https://img.shields.io/badge/Status-Completed-green)

---

## 📋 Task Overview

**Task:** API Security Risk Analysis  
**APIs Tested:** reqres.in | jsonplaceholder.typicode.com  
**Tool Used:** Postman v12.8.4  
**Methodology:** OWASP API Security Top 10 (2023)  
**Assessment Date:** May 2, 2026  
**Intern:** Mohammad Sami Sadiq Ali Sayed  

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| Postman v12.8.4 | API request testing & response analysis |
| Browser DevTools | Security header inspection |
| reqres.in | Test API for authentication testing |
| jsonplaceholder.typicode.com | Test API for authorization testing |

---

## 🔍 Vulnerabilities Found

| # | Finding | Risk | OWASP API | Status |
|---|---------|------|-----------|--------|
| 1 | Unauthenticated PII Exposure — GET /users | 🔴 CRITICAL | API1:2023 | Confirmed |
| 2 | Open Data Access — GET /posts (No Auth) | 🟠 HIGH | API2:2023 | Confirmed |
| 3 | Verbose Error Message Disclosure | 🟠 HIGH | API8:2023 | Confirmed |
| 4 | Missing Input Validation on Login | 🟡 MEDIUM | API8:2023 | Confirmed |
| 5 | No Rate Limiting on Endpoints | 🟡 MEDIUM | API4:2023 | Identified |
| 6 | Missing HTTP Security Headers | 🟢 LOW | API8:2023 | Identified |

---

## 💥 Key Findings with Evidence

### Finding 1 — Unauthenticated PII Exposure (CRITICAL)
```
GET https://jsonplaceholder.typicode.com/users
Response: 200 OK — No authentication required
```
**Data Exposed:** Full name, email, address, phone, geolocation, company — for ALL users  
📸 *[Screenshot: Image 1 — GET /users 200 OK with full PII, zero authentication]*

---

### Finding 2 — Open Data Access (HIGH)
```
GET https://jsonplaceholder.typicode.com/posts
Response: 200 OK — 100 posts returned — No authentication
```
**Impact:** All application data accessible anonymously — 7.99 KB in 161ms  
📸 *[Screenshot: Image 2 — GET /posts 200 OK, no auth headers sent]*

---

### Finding 3 — Verbose Error Disclosure (HIGH)
```
POST https://reqres.in/api/login
Response: 401 Unauthorized — But reveals:
- Internal header name: x-api-key
- Authentication architecture: /api/* vs /app/* endpoint distinction  
- Working curl command with exact syntax
- API key acquisition URL
```
📸 *[Screenshot: Image 3 — 401 revealing full API authentication architecture]*

---

### Finding 4 — Missing Input Validation (MEDIUM)
```
POST https://reqres.in/api/login
Payload: { "email": "" }
Response: 401 — Same verbose response — No validation rejection
```
**Impact:** Malformed input processed without rejection  
📸 *[Screenshot: Image 4 — Empty email accepted, processed, returns same 401]*

---

## 🛡️ Remediation Summary

| Priority | Action |
|----------|--------|
| 🔴 Immediate | Add authentication & authorization to all user data endpoints |
| 🟠 7 Days | Replace verbose errors with generic messages |
| 🟠 7 Days | Implement server-side input validation |
| 🟡 30 Days | Add rate limiting with account lockout |
| 🟢 90 Days | Add missing HTTP security headers |

---

## 📁 Repository Contents

```
FUTURE_CS_03/
├── README.md                                  # This file
├── FUTURE_CS_03_API_Security_Report.docx      # Full API security report
└── screenshots/
    ├── 01_users_pii_exposure.png              # Finding 1 — PII exposure
    ├── 02_posts_open_access.png               # Finding 2 — Open data
    ├── 03_verbose_error_disclosure.png        # Finding 3 — Verbose errors
    └── 04_missing_input_validation.png        # Finding 4 — No validation
```

---

## 👤 About the Intern

**Mohammad Sami Sadiq Ali Sayed**  
BSc IT Graduate | CGPA: 8.43 | Aspiring Penetration Tester  
📧 sayedsami86@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/mohammed-sami-sayed-b702673b7)  
🔗 [Task 1 — VA Report](https://github.com/sayedsami86/FUTURE_CS_01)  
🔗 [Task 2 — Phishing Detection](https://github.com/sayedsami86/FUTURE_CS_02)  

---

*This assessment was performed on public test APIs in a controlled environment for educational purposes as part of the Future Interns Cyber Security Internship Program.*
