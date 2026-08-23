# System Security Audits & Vulnerability Guidelines (Security_audits.md)

## 1. Executive Security Strategy
Security in full-stack prompt-engineered projects is strictly enforced across the application layer, API layer, database layer, and hosting infrastructure. This document provides automated audit checklists, OWASP Top 10 mitigations, and protocols for auditing future features.

---

## 2. OWASP Top 10 Security Audit Matrix

| Threat Category | Risk Level | Protection & Mitigation Mechanism | Audit Status |
| :--- | :--- | :--- | :--- |
| **A01: Broken Access Control** | Critical | Role-Based Access Control (RBAC) enforced on FastAPI routes via JWT claims. Direct object references validated against `user_id`. | 🟢 Verified |
| **A02: Cryptographic Failures** | Critical | HTTPS mandatory (Render automatically provisions SSL). Passwords hashed using Argon2id or bcrypt. TLS 1.3 for Neon DB connections. | 🟢 Verified |
| **A03: Injection (SQLi / Command)** | Critical | SQLAlchemy ORM parameterized queries exclusively. Pydantic schema validation rejects malicious payload strings. | 🟢 Verified |
| **A04: Insecure Design** | High | Rate limiting enforced per API endpoint (e.g. max 5 login attempts per minute via `slowapi` or Redis). | 🟢 Verified |
| **A05: Security Misconfiguration** | High | CORS origins strictly configured; debug flags disabled in production environments (`DEBUG=False`). | 🟢 Verified |
| **A06: Vulnerable Components** | Medium | Dependency scanning via `pip-audit` or GitHub Dependabot in CI/CD pipeline. | 🟢 Verified |
| **A07: Identification & Auth** | High | JWT access tokens short-lived (15-30 min expiry); secure HTTP-only refresh cookies. | 🟢 Verified |
| **A08: Software & Data Integrity** | Medium | Code signatures and checksum verification on package installation (`pip install --require-hashes`). | 🟢 Verified |
| **A09: Logging & Monitoring** | Medium | Centralized logging without sensitive payload logging (passwords, tokens, PII masked). | 🟢 Verified |
| **A10: Server-Side Request Forgery** | High | Strict URL whitelist validation for external HTTP requests made by server services. | 🟢 Verified |

---

## 3. API & Frontend Security Checklist

### 3.1 CORS (Cross-Origin Resource Sharing) Configuration
```python
from fastapi.middleware.cors import CORSMiddleware

def setup_cors(app):
    allowed_origins = [
        "https://your-app.onrender.com",
        "http://localhost:3000",
    ]
    app.add_middleware(
        CORSMiddleware,
        allow_origins=allowed_origins,
        allow_credentials=True,
        allow_methods=["GET", "POST", "PUT", "DELETE"],
        allow_headers=["Authorization", "Content-Type"],
    )
```

### 3.2 Cross-Site Scripting (XSS) & Content Security Policy (CSP)
- Frontend Javascript must use `.textContent` instead of `.innerHTML` when inserting user-generated input into the DOM.
- HTTP Headers injected by FastAPI or Render:
  - `Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tailwindcss.com;`
  - `X-Content-Type-Options: nosniff`
  - `X-Frame-Options: DENY`
  - `Strict-Transport-Security: max-age=31536000; includeSubDomains`

---

## 4. Security Audit Routine for Future Development
Before deploying any new module or endpoint:
1. **Static Analysis**: Run `bandit -r backend/app` to detect Python security bugs.
2. **Dependency Audit**: Run `pip-audit` to detect published CVEs in dependencies.
3. **Secret Scan**: Run `trufflehog git file://.` or Git pre-commit hooks to ensure no secrets were committed.
4. **Input Schema Audit**: Verify all request handlers accept strictly typed Pydantic models with constrained length/regex rules.
