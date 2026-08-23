# System Rules & Guidelines (Rules.md)

## 1. Core Principles & Philosophy
This repository operates under strict engineering standards. All code generated or written manually must follow modular, self-documenting, and secure patterns.

---

## 2. Rules: What to Implement vs. What to Avoid

### 🟢 What to Implement (Best Practices)
1. **Strict Type Annotations**: Use Python `typing` module and Pydantic schemas for all API payloads and internal functions.
2. **Explicit Environment Configuration**: Store all credentials, API keys, and database URIs in `.env` files accessed via Pydantic `BaseSettings`.
3. **Structured Error Responses**: Always return JSON errors with standardized structures: `{ "success": false, "error": { "code": "ERROR_CODE", "message": "Human readable detail" } }`.
4. **Parameterized SQL / ORM**: Use SQLAlchemy ORM or parameterized queries exclusively to prevent SQL injection.
5. **Stateless API Design**: Keep API routes stateless using JWT tokens or database-backed sessions.
6. **Mobile-First CSS**: Write Tailwind classes using mobile-first breakpoints (`sm:`, `md:`, `lg:`).

### 🔴 What to Avoid (Anti-Patterns)
1. **NEVER Hardcode Secrets**: No raw passwords, secret keys, or Neon DB connection strings committed to Git.
2. **NEVER Swallow Exceptions**: Do not use empty `except:` or silent `catch(err) {}` blocks without logging or standard error reporting.
3. **NEVER Mutate Global State Directly**: Avoid global variables in Python or mutating external DOM states outside dedicated JS state objects.
4. **NEVER Bypass Backend Validation**: Client-side validation is UI feedback only; the backend must re-validate every field and action.
5. **NEVER Mix Logic and Presentation**: Keep HTML files clean; delegate interactive logic to external JS modules and styles to Tailwind CSS.

---

## 3. Error Handling Protocol

### 3.1 Backend Exception Standard (FastAPI / Flask)
```python
from fastapi import HTTPException, status, Request
from fastapi.responses import JSONResponse

class AppException(Exception):
    def __init__(self, status_code: int, error_code: str, message: str):
        self.status_code = status_code
        self.error_code = error_code
        self.message = message

async def app_exception_handler(request: Request, exc: AppException):
    return JSONResponse(
        status_code=exc.status_code,
        content={
            "success": False,
            "error": {
                "code": exc.error_code,
                "message": exc.message
            }
        }
    )
```

### 3.2 Standard HTTP Status Codes
- `200 OK`: Request succeeded.
- `201 Created`: Resource created successfully.
- `400 Bad Request`: Validation failure or bad request payload.
- `401 Unauthorized`: Missing or invalid JWT authentication token.
- `403 Forbidden`: Authenticated user lacks permission.
- `404 Not Found`: Requested resource does not exist.
- `422 Unprocessable Entity`: Pydantic schema validation failure.
- `500 Internal Server Error`: Unhandled server-side error (must log stack trace internally, return sanitized message to user).

---

## 4. Prompt Engineering Rules for AI Generators
1. **Context-First Prompting**: Provide system role, schema references, and expected output formats in every prompt.
2. **No Hallucinated Imports**: Only reference verified standard library packages or libraries declared in `requirements.txt`.
3. **Incremental Code Generation**: Request implementation block-by-block (Model -> Schema -> Service -> API Route -> Frontend UI).
4. **Self-Correction & Linting**: Always instruct the AI agent to verify syntax, non-null checks, and type signatures before outputting final code.
