# Full Stack Prompt Engineering Strategy & Specification

Welcome to the **Full Stack Prompt Engineering for Projects** repository. This workspace provides a comprehensive, production-grade strategy suite for building, auditing, and deploying modern full-stack web applications.

---

## Tech Stack & Application Ecosystem Directory

Direct links to all official platforms, tools, and libraries utilized in this architecture:

### Backend Engine & Frameworks
- [**Python 3.11+**](https://www.python.org/) - Primary server-side programming language.
- [**FastAPI**](https://fastapi.tiangolo.com/) - Modern, high-performance web framework for building REST APIs with Python 3.8+ based on standard Python type hints.
- [**Flask**](https://flask.palletsprojects.com/) - Lightweight WSGI web application framework.
- [**SQLAlchemy**](https://www.sqlalchemy.org/) - Python SQL toolkit and Object Relational Mapper (ORM).
- [**Alembic**](https://alembic.sqlalchemy.org/) - Lightweight database migration tool for usage with SQLAlchemy.
- [**Pydantic**](https://docs.pydantic.dev/) - Data validation using Python type annotations.
- [**Pytest**](https://docs.pytest.org/) - Python testing framework for unit and integration test suites.

### Database & Cloud Infrastructure
- [**PostgreSQL**](https://www.postgresql.org/) - World's most advanced open-source relational database.
- [**Neon DB**](https://neon.tech/) - Serverless PostgreSQL with instant branching, autoscaling, and point-in-time recovery.
- [**Render**](https://render.com/) - Cloud platform to build and run web services, background workers, and static sites.
- [**Vercel**](https://vercel.com/) - Frontend cloud platform for static site edge CDN deployment and serverless routing.

### Authentication & Push Notifications
- [**Firebase Authentication**](https://firebase.google.com/docs/auth) - Authentication system supporting Google OAuth, email/password, and JWT custom claims.
- [**Firebase Admin Python SDK**](https://firebase.google.com/docs/admin/setup) - Server-side SDK for ID token verification and custom claims.
- [**Firebase Cloud Messaging (FCM)**](https://firebase.google.com/docs/cloud-messaging) - Cross-platform messaging solution for push notifications.

### Frontend UI & Design System
- [**HTML5 (MDN)**](https://developer.mozilla.org/en-US/docs/Web/HTML) - Semantic markup standard.
- [**Tailwind CSS**](https://tailwindcss.com/) - Utility-first CSS framework for rapid UI development.
- [**JavaScript (MDN)**](https://developer.mozilla.org/en-US/docs/Web/JavaScript) - Lightweight, interpreted client-side programming language.
- [**Coolors App**](https://coolors.co/) - Superfast color palette generator and WCAG contrast checker.
- [**Google Fonts**](https://fonts.google.com/) - Library of 1,500+ open-source font families (Plus Jakarta Sans, Fira Code, Outfit).
- [**Google Material Symbols & Icons**](https://fonts.google.com/icons) - Variable icon font system.
- [**Figma**](https://www.figma.com/) - Collaborative interface design and prototyping tool.
- [**Google Stitch AI**](https://stitch.withgoogle.com/) - Prompt-driven UI generation tool.

### Security, Audit & Ops
- [**OWASP Top 10**](https://owasp.org/www-project-top-ten/) - Standard awareness document for developers and web application security.
- [**Bandit**](https://bandit.readthedocs.io/) - Tool designed to find common security issues in Python code.
- [**pip-audit**](https://pypa.github.io/pip-audit/) - Tool for auditing Python environments for known vulnerabilities.
- [**TruffleHog**](https://trufflehog.org/) - Secret scanner for detecting leaked credentials and API keys.
- [**Git**](https://git-scm.com/) - Distributed version control system.
- [**GitHub**](https://github.com/) - Cloud platform for code hosting, version control, and CI/CD pipelines.

---

## Strategy Documentation Map

The system strategy is modularized across 13 core markdown specification documents:

1. [**`PRD.md`**](PRD.md) - **Project Requirement Document**: Vision, target audience, key feature specifications, and core building logic.
2. [**`Architecture.md`**](Architecture.md) - **System Architecture**: Directory layout, component flow, Neon DB connection pooling, and Render deployment configuration.
3. [**`Rules.md`**](Rules.md) - **Development Rules**: Coding standards, best practices, anti-patterns (what to avoid), error handling standards, and prompt rules.
4. [**`Phases.md`**](Phases.md) - **Project Roadmap**: 5-phase execution plan from scaffolding to auth, core engine, frontend styling, and production deployment.
5. [**`Designs.md`**](Designs.md) - **Frontend Design System**: Color tokens, Tailwind CSS rules, HTML templates, and design ingestion workflows (Stitch AI, Figma MCP, Manual).
6. [**`Memory.md`**](Memory.md) - **AI System Memory**: AGY implementation plan tracking, state preservation, decisions log, and session memory context.
7. [**`Skill.md`**](Skill.md) - **Prompt Engineering Skills**: Stored AI logic, system prompt templates, task execution blueprints, and subagent delegation workflows.
8. [**`Security_audits.md`**](Security_audits.md) - **System Security Audits**: OWASP Top 10 mitigation checklist, CORS policies, XSS/CSP headers, and static analysis workflows.
9. [**`Security_db.md`**](Security_db.md) - **Database Security & DLP**: Neon DB TLS 1.3 encryption, database branching, point-in-time recovery (PITR), and SQL injection defenses.
10. [**`Authentication.md`**](Authentication.md) - **Authentication & Firebase Integration**: Firebase Auth, Firebase Admin SDK, JWT verification, custom claims, and auth middleware.
11. [**`Color_theory.md`**](Color_theory.md) - **Color Theory & Palette Strategy**: Coolors.co integration, 60-30-10 rule, Tailwind palette mapping, and WCAG contrast rules.
12. [**`Typography_icons.md`**](Typography_icons.md) - **Typography & Icons Strategy**: Google Fonts (Plus Jakarta Sans, Fira Code, Outfit), Tailwind font config, and Google Material Symbols integration.
13. [**`Deployment_vercel.md`**](Deployment_vercel.md) - **Frontend Vercel Deployment**: Vercel Edge CDN configuration, `vercel.json` rewrites, env variables, GitHub branch previews, and Render CORS sync.

---

## Quickstart & Deployment Flow

### 1. Local Scaffolding
```bash
# Clone the repository
git clone https://github.com/parthongit89/Project-Strategies-Prompt-engineering-.git
cd Project-Strategies-Prompt-engineering-

# Set up Python virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r backend/requirements.txt
```

### 2. Environment Configuration
Create a `.env` file in the `backend/` folder based on `.env.example`:
```ini
DATABASE_URL=postgresql://user:password@ep-xxx-pooler.neon.tech/neondb?sslmode=require
SECRET_KEY=your_super_secret_jwt_key
ALGORITHM=HS256
CORS_ORIGINS=https://your-app.vercel.app,https://your-app.onrender.com
```

### 3. Deploy to Render, Vercel & Neon DB
1. Provision a PostgreSQL instance on [**Neon DB**](https://neon.tech/) and copy the pooled connection string.
2. Deploy the backend API to [**Render**](https://render.com/). Set build command: `pip install -r requirements.txt && alembic upgrade head` and start command: `uvicorn app.main:app --host 0.0.0.0 --port $PORT`.
3. Deploy the frontend to [**Vercel**](https://vercel.com/) with GitHub automatic branch preview integration.
