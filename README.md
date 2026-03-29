# FUTURE_CS_01
# 🔐 Vulnerability Assessment Report

## 📍 Target
**OWASP Juice Shop (Heroku)** = https://juice-shop.herokuapp.com/

## 🛠 Tools Used
- Nmap  
- OWASP ZAP (Passive Scan)  
- Browser DevTools  

---

## 📌 Executive Summary

- Security assessment performed on Juice Shop web application.  
- **Goal:** Identify vulnerabilities, classify risks, and suggest fixes.  
- **Findings:** Multiple missing security headers, information disclosure, and session management issues.  

---

## 🛠 Methodology

- **Nmap** → Checked open ports and services.  
- **nslookup** → Verified DNS resolution and hosting IPs.  
- **OWASP ZAP (Passive Scan)** → Captured traffic and flagged vulnerabilities.  
- **Browser DevTools** → Confirmed headers, cookies, and local storage behavior.  

---

## 🔎 Reconnaissance Findings (Nmap)

- Port **80/tcp** open on local router (GoAhead WebServer).  
- Juice Shop resolves to multiple Heroku IPs.  
- **Risk Level:** Low (expected behavior, but shows exposure).  

---

## ⚠️ Vulnerabilities Detected (ZAP)

- Application Error Disclosure → Error messages reveal technical details.  
- Missing Security Headers → No CSP, HSTS, or X-Frame-Options.  
- Cross-Domain Misconfiguration (CORS) → `Access-Control-Allow-Origin: *`.  
- Session ID in URL → Tokens visible in URL.  
- Information Disclosure (Debug Errors) → Sensitive error messages exposed.  
- Timestamp Disclosure → Unix timestamps in responses.  
- Weak Cache-Control → Insecure caching directives.  
- X-Content-Type-Options Missing → No protection against MIME sniffing.  

---

## 📊 Risk Classification

- **High Risk:**
  - Missing CSP/HSTS  
  - Session IDs in URL  

- **Medium Risk:**
  - Error disclosure  
  - CORS misconfiguration  
  - Missing anti-clickjacking protections  

- **Low Risk:**
  - Timestamp disclosure  
  - Weak cache-control  

---

## ✅ Recommendations

- Add modern security headers:
  - Content Security Policy (CSP)  
  - HTTP Strict Transport Security (HSTS)  
  - X-Frame-Options  
  - X-Content-Type-Options  

- Restrict CORS to trusted domains.  
- Replace detailed error messages with generic ones.  
- Improve session handling (avoid tokens in URLs).  
- Strengthen cache-control and remove unnecessary metadata.  
- Regularly patch and update hosting/server configurations.  

---

## 📌 Conclusion

- Juice Shop is functional but lacks several basic protections.  
- Most issues are easy to fix but critical for security.  
- Addressing these vulnerabilities will significantly improve resilience against common attacks.  
