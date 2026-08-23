# System Architecture & Tech Stack (Architecture.md)

## 1. Technology Stack Overview

| Layer | Technology | Description |
| :--- | :--- | :--- |
| **Backend Framework** | Python 3.11+ (FastAPI or Flask) | High-performance asynchronous API engine with Pydantic schemas |
| **Database** | PostgreSQL on Neon DB | Serverless, autoscaling PostgreSQL with branching support |
| **Database ORM** | SQLAlchemy 2.0 / SQLModel | Async-capable Object Relational Mapper |
| **Hosting & Infra** | Render | Managed Web Service & Static Site hosting |
| **Frontend UI** | HTML5, Tailwind CSS v3, JavaScript | Lightweight, zero-build or Vite-assisted frontend framework |
| **Design Ingestion** | Stitch AI / Figma MCP | Prompt-driven & MCP-assisted UI design generation |
| **Version Control** | Git & GitHub | Source code control & automated deployment triggers |

---

## 2. Recommended Directory Structure

```
project-root/
├── .github/
│   └── workflows/
│       └── deploy.yml          # CI/CD workflow for Render
├── backend/
│   ├── app/
│   │   ├── api/
│   │   │   ├── v1/
│   │   │   │   ├── endpoints/
│   │   │   │   │   ├── auth.py
│   │   │   │   │   ├── users.py
│   │   │   │   │   └── game.py
│   │   │   │   └── api.py
│   │   ├── core/
│   │   │   ├── config.py       # Pydantic Settings & Env management
│   │   │   ├── database.py     # Neon DB connection & sessionmaker
│   │   │   └── security.py     # Password hashing & JWT logic
│   │   ├── models/             # SQLAlchemy DB Models
│   │   │   ├── user.py
│   │   │   └── game_state.py
│   │   ├── schemas/            # Pydantic Request/Response models
│   │   │   ├── auth.py
│   │   │   └── user.py
│   │   ├── services/           # Business logic & game engine algorithms
│   │   │   ├── auth_service.py
│   │   │   └── engine.py
│   │   └── main.py             # FastAPI / Flask app initialization
│   ├── tests/                  # Pytest test suite
│   ├── alembic/                 # DB Migration scripts
│   ├── alembic.ini
│   ├── requirements.txt
│   └── render.yaml             # Render infrastructure-as-code specification
├── frontend/
│   ├── public/
│   │   ├── assets/
│   │   │   ├── css/
│   │   │   │   └── tailwind.css
│   │   │   ├── js/
│   │   │   │   ├── app.js
│   │   │   │   ├── auth.js
│   │   │   │   └── api_client.js
│   │   │   └── images/
│   │   └── index.html
│   ├── tailwind.config.js
│   └── index.html
├── docs/
│   ├── PRD.md
│   ├── Architecture.md
│   ├── Rules.md
│   ├── Phases.md
│   ├── Designs.md
│   ├── Memory.md
│   ├── Skill.md
│   ├── Security_audits.md
│   └── Security_db.md
├── README.md
└── .gitignore
```

---

## 3. Component Architecture & Data Flow

```mermaid
graph TD
    subgraph Frontend["Frontend Client (Render Static Site / CDN)"]
        UI[HTML5 / Tailwind CSS]
        JS[JavaScript Client / Fetch API]
    end

    subgraph Infrastructure["Render Cloud Platform"]
        API[FastAPI / Flask Application]
        Gunicorn[Gunicorn / Uvicorn Server Engine]
    end

    subgraph Database["Neon DB Platform"]
        NeonDB[(PostgreSQL Database)]
        Pooling[Neon Connection Pooler]
    end

    UI --> JS
    JS -->|REST API / HTTPS| API
    API --> Gunicorn
    API -->|SQLAlchemy / asyncpg| Pooling
    Pooling --> NeonDB
```

---

## 4. Neon DB & Database Architecture
- **Connection Mode**: SSL mode `require` mandatory.
- **Connection Pooling**: Use Neon's PgBouncer pooled connection string (`postgresql://user:pass@ep-xxx-pooler.neon.tech/dbname?sslmode=require`) for FastAPI stateless connections.
- **Migrations**: Managed via `alembic` (Alembic configuration linked to SQLAlchemy models).

---

## 5. Render Deployment Architecture
- **Web Service Configuration**:
  - **Environment**: Python 3.11
  - **Build Command**: `pip install -r requirements.txt && alembic upgrade head`
  - **Start Command**: `uvicorn app.main:app --host 0.0.0.0 --port $PORT`
  - **Health Check Path**: `/health` or `/api/v1/health`
- **Environment Variables**:
  - `DATABASE_URL`: Connection string from Neon DB
  - `SECRET_KEY`: Secret string for JWT generation
  - `ALGORITHM`: `HS256`
  - `CORS_ORIGINS`: Allowed frontend domains
