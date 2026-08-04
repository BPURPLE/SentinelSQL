# SentinelSQL Folder Structure

**Version:** 1.0 (MVP)  
**Status:** Design Freeze

---

# 1. Purpose

This document defines the official repository structure for SentinelSQL.

The repository is organized to reflect the approved Product Specification, Software Architecture, Database Schema, and API Contract.

Every directory has a single responsibility.

No folder may contain functionality outside its defined scope.

---

# 2. Repository Structure

```text
SentinelSQL/
│
├── README.md
├── LICENSE
├── .gitignore
├── .env.example
├── requirements.txt
├── docker-compose.yml
│
├── docs/
│   ├── product_specification.md
│   ├── architecture.md
│   ├── database_schema.md
│   ├── api_contract.md
│   ├── folder_structure.md
│   ├── engineering_principles.md
│   └── roadmap.md
│
├── backend/
│   ├── main.py
│   │
│   ├── api/
│   │
│   ├── auth/
│   │
│   ├── middleware/
│   │
│   ├── gateway/
│   │
│   ├── detection/
│   │   ├── rule_engine.py
│   │   ├── ml_classifier.py
│   │   ├── decision_engine.py
│   │   └── response_engine.py
│   │
│   ├── ai/
│   │
│   ├── database/
│   │
│   ├── schemas/
│   │
│   ├── config/
│   │
│   ├── services/
│   │
│   └── utils/
│
├── frontend/
│   ├── public/
│   └── src/
│
├── tests/
│
├── docker/
│
└── .github/
    └── workflows/
```

---

# 3. Root Directory

The repository root contains project-wide configuration and documentation.

| Item | Purpose |
|------|---------|
| README.md | Project overview |
| LICENSE | Project license |
| .gitignore | Git exclusions |
| .env.example | Environment variable template |
| requirements.txt | Python dependencies |
| docker-compose.yml | Local development configuration |

---

# 4. Documentation

```
docs/
```

Contains all frozen design documentation.

| File | Purpose |
|------|---------|
| product_specification.md | Product definition |
| architecture.md | Software architecture |
| database_schema.md | Database design |
| api_contract.md | REST API contract |
| folder_structure.md | Repository organization |
| engineering_principles.md | Development standards |
| roadmap.md | Project milestones |

No implementation code belongs in this directory.

---

# 5. Backend

```
backend/
```

Contains all server-side application logic.

---

## main.py

Application entry point.

Responsible for:

- Starting the FastAPI application.
- Registering routers.
- Initializing middleware.

---

## api/

Contains API endpoint implementations.

Responsibilities

- Receive HTTP requests.
- Return HTTP responses.
- Delegate business logic.

API routes must not contain business logic.

---

## auth/

Contains authentication and authorization components.

Responsibilities

- JWT authentication.
- Password verification.
- Role-Based Access Control.

---

## middleware/

Contains request-processing middleware.

Responsibilities

- Rate limiting.
- Request interception.
- Request lifecycle handling.

---

## gateway/

Implements the SQL Gateway.

Responsibilities

- Intercept SQL queries.
- Canonicalize SQL.
- Tokenize SQL.
- Extract ML features.

No detection logic belongs here.

---

## detection/

Implements the Detection Layer.

Contains

- rule_engine.py
- ml_classifier.py
- decision_engine.py
- response_engine.py

Responsibilities

### rule_engine.py

Detect known SQL Injection patterns using deterministic rules.

---

### ml_classifier.py

Generate TF-IDF vectors and classify SQL queries using Multinomial Naive Bayes.

---

### decision_engine.py

Generate the final deterministic security decision.

Possible outcomes

- ALLOW
- BLOCK

---

### response_engine.py

Execute the Threat Decision Engine decision.

Responsibilities

- Forward approved queries.
- Reject blocked queries.
- Trigger alerts.
- Trigger audit logging.

---

## ai/

Contains the AI explanation pipeline.

Responsibilities

- Prompt Guard.
- AI Threat Explainer.
- Output Validation.

The AI subsystem is advisory only.

---

## database/

Contains database configuration.

Responsibilities

- Database connection.
- Database session management.
- ORM models.

---

## schemas/

Contains Pydantic models.

Responsibilities

- Request validation.
- Response validation.

---

## config/

Contains application configuration.

Responsibilities

- Environment configuration.
- Security settings.
- Application constants.

Sensitive values must never be hardcoded.

---

## services/

Contains reusable business services.

Responsibilities

- Audit logging.
- Dashboard aggregation.
- Report generation.

---

## utils/

Contains shared utility functions.

Utilities must remain generic and reusable.

---

# 6. Frontend

```
frontend/
```

Contains the React application.

---

## public/

Static assets.

---

## src/

Frontend source code.

Responsibilities

- Authentication interface.
- Dashboard.
- Incident viewer.
- Reports.

The frontend never communicates directly with PostgreSQL.

---

# 7. Tests

```
tests/
```

Contains automated tests.

Testing categories include:

- Authentication
- Gateway
- Detection
- API
- End-to-End

No production code belongs here.

---

# 8. Docker

```
docker/
```

Contains Docker-related files used for local development.

---

# 9. GitHub

```
.github/workflows/
```

Contains GitHub Actions workflows.

Responsibilities

- Continuous Integration.
- Automated testing.

---

# 10. Dependency Rules

The repository follows a strict dependency hierarchy.

```
Frontend
        │
        ▼
API
        │
        ▼
Authentication
        │
        ▼
Gateway
        │
        ▼
Detection
        │
        ▼
Decision Engine
        │
        ▼
Response Engine
        │
        ▼
Database
```

Higher layers may depend on lower layers.

Lower layers must never depend on higher layers.

---

# 11. Folder Responsibilities

Each directory has one clearly defined responsibility.

Business logic must never be duplicated.

Cross-module communication must occur only through well-defined interfaces.

Implementation must remain consistent with the approved Software Architecture.

---

# 12. Structure Freeze

This document defines the official SentinelSQL repository structure.

All implementation must conform to this structure.

Structural changes require explicit approval before implementation.