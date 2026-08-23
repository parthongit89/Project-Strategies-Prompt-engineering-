# AI System Memory & State Tracking (Memory.md)

## 1. Overview & AGY Integration
`Memory.md` serves as the persistent memory state reference for Antigravity (AGY) and AI agentic sessions. While AGY automatically maintains runtime implementation plans in `.system_generated/` and context logs, this document defines explicit architectural conventions and memory protocols for long-term project persistence.

---

## 2. AGY Implementation Plan Lifecycle
- **Plan Generation**: When a complex architectural change or feature is requested, AGY creates an `implementation_plan.md` artifact under the conversation brain path.
- **User Review Checkpoint**: AGY pauses for explicit user approval before mutating codebase state.
- **Execution Tracking**: Completed steps in the implementation plan are updated dynamically.
- **Walkthrough Artifact**: Once work is verified, AGY builds a `walkthrough.md` artifact detailing tested functionality, terminal logs, and code diffs.

---

## 3. Active Context & System Memory Log

### 3.1 Tech Stack & Active Configuration
- **Backend Framework**: Python (FastAPI / Flask)
- **Database Engine**: Neon PostgreSQL (`postgresql://...neon.tech...`)
- **Deployment Host**: Render Managed Web Service
- **Frontend Stack**: Semantic HTML5, Tailwind CSS, Vanilla JS
- **Version Control**: Git / GitHub repo tracking `main` branch

### 3.2 Key Architectural Decisions
1. **Database Connection Pooling**: Neon DB connections must use connection pooling via PgBouncer for stateless serverless functions/workers.
2. **Authentication**: JWT tokens passed via `Authorization: Bearer <token>` HTTP headers. Passwords hashed using Argon2 / bcrypt.
3. **UI Workflow**: Modular vanilla JS scripts split into `api_client.js`, `auth.js`, and `app.js` without heavy framework dependencies.

---

## 4. Context Preservation Checklist for AI Agents
When starting a new session or executing complex subagent tasks:
- [ ] Read `PRD.md` to align on product intent.
- [ ] Read `Architecture.md` to respect folder boundaries and import paths.
- [ ] Read `Rules.md` to strictly enforce coding and error handling protocols.
- [ ] Inspect existing git log and active `implementation_plan.md` before applying edits.
