# Full Stack Prompt Engineering Strategy & Specification

Welcome to the **Full Stack Prompt Engineering for Projects** repository. This workspace provides a comprehensive, production-grade strategy suite for building, auditing, and deploying modern full-stack web applications.

---

## 🚀 Tech Stack Matrix

- **Backend**: Python 3.11+ (FastAPI / Flask)
- **Database**: PostgreSQL hosted on [Neon DB](https://neon.tech) (Serverless, Branching, SSL/TLS)
- **Deployment & Hosting**: Managed Web Services on [Render](https://render.com)
- **Frontend**: HTML5, Tailwind CSS, JavaScript (Vanilla / Modern JS)
- **UI Ingestion Workflows**: Google Stitch AI Prompts, Figma + MCP Server Integration, Manual Custom Designs
- **Security & Reliability**: Automated OWASP Audits, Neon DB PITR Disaster Recovery, Alembic Migrations

---

## 📖 Strategy Documentation Map

The system strategy is modularized across 9 core markdown specification documents:

1. 📄 [**`PRD.md`**](PRD.md) - **Project Requirement Document**: Vision, target audience, key feature specifications, and core building logic.
2. 🏗️ [**`Architecture.md`**](Architecture.md) - **System Architecture**: Directory layout, component flow, Neon DB connection pooling, and Render deployment configuration.
3. 📜 [**`Rules.md`**](Rules.md) - **Development Rules**: Coding standards, best practices, anti-patterns (what to avoid), error handling standards, and prompt rules.
4. 🗺️ [**`Phases.md`**](Phases.md) - **Project Roadmap**: 5-phase execution plan from scaffolding to auth, core engine, frontend styling, and production deployment.
5. 🎨 [**`Designs.md`**](Designs.md) - **Frontend Design System**: Color tokens, Tailwind CSS rules, HTML templates, and design ingestion workflows (Stitch AI, Figma MCP, Manual).
6. 🧠 [**`Memory.md`**](Memory.md) - **AI System Memory**: AGY implementation plan tracking, state preservation, decisions log, and session memory context.
7. ⚡ [**`Skill.md`**](Skill.md) - **Prompt Engineering Skills**: Stored AI logic, system prompt templates, task execution blueprints, and subagent delegation workflows.
8. 🛡️ [**`Security_audits.md`**](Security_audits.md) - **System Security Audits**: OWASP Top 10 mitigation checklist, CORS policies, XSS/CSP headers, and static analysis workflows.
9. 🔐 [**`Security_db.md`**](Security_db.md) - **Database Security & DLP**: Neon DB TLS 1.3 encryption, database branching, point-in-time recovery (PITR), and SQL injection defenses.

---

## 🛠️ Quickstart & Deployment Flow

### 1. Local Scaffolding
```bash
# Clone the repository
git clone https://github.com/your-username/project-strategy.git
cd project-strategy

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
CORS_ORIGINS=https://your-app.onrender.com
```

### 3. Deploy to Render & Neon DB
1. Provision a PostgreSQL instance on **Neon DB** and copy the pooled connection string.
2. Link your GitHub repository to **Render**.
3. Set the build command to `pip install -r requirements.txt && alembic upgrade head`.
4. Set the start command to `uvicorn app.main:app --host 0.0.0.0 --port $PORT`.
