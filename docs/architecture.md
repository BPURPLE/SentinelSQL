# SentinelSQL Software Architecture

**Version:** 1.0 (MVP)  
**Status:** Design Freeze

---

# 1. Purpose

This document defines the software architecture of SentinelSQL.

It specifies the responsibilities of every system component, the request lifecycle, communication between modules, and the security boundaries enforced throughout the application.

This document is the authoritative architectural reference for implementation.

No implementation may contradict this architecture without explicit approval.

---

# 2. Architectural Style

SentinelSQL follows a modular layered architecture.

Each layer has exactly one responsibility.

Communication always flows downward.

No layer may bypass another layer.

```
Client Request
        │
        ▼
Rate Limiter
        │
        ▼
Authentication
        │
        ▼
Authorization
        │
        ▼
Validation
        │
        ▼
Gateway Layer
        │
        ▼
Detection Layer
        │
        ▼
Threat Decision Engine
        │
        ▼
Response Engine
        │
        ▼
Database
        │
        ▼
Audit Logging
        │
        ▼
AI Prompt Guard
        │
        ▼
AI Threat Explainer
        │
        ▼
Output Validator
        │
        ▼
Dashboard & Reports
```

---

# 3. High-Level Components

## Client

The client represents the CRUD application communicating with SentinelSQL through authenticated API requests.

The client never communicates directly with the database.

---

## Rate Limiter

Responsibilities

- Limit excessive requests.
- Reduce brute-force attacks.
- Mitigate request flooding.

Every incoming request passes through this layer.

---

## Authentication

Responsibilities

- Validate JWT tokens.
- Authenticate users.
- Establish user identity.

Unauthenticated requests are rejected immediately.

---

## Authorization

Responsibilities

- Enforce Role-Based Access Control (RBAC).
- Verify permissions.
- Restrict access according to user role.

---

## Validation

Responsibilities

- Validate request schemas.
- Validate data types.
- Validate request length.
- Reject malformed requests.

Validation is performed using Pydantic models.

---

## Gateway Layer

The Gateway Layer intercepts every SQL query before database execution.

Components

- Interceptor
- Canonicalizer
- Tokenizer
- Feature Extractor

Responsibilities

- Intercept SQL queries.
- Normalize SQL syntax.
- Tokenize SQL statements.
- Extract machine-learning features.

No SQL query reaches PostgreSQL without passing through this layer.

---

## Detection Layer

The Detection Layer evaluates every SQL query.

It consists of two independent detection engines.

### Rule Engine

Responsibilities

- Detect known SQL Injection attacks.
- Apply deterministic detection rules.
- Produce rule-based detection results.

### ML Classifier

Responsibilities

- Convert SQL queries into TF-IDF feature vectors.
- Classify SQL queries using Multinomial Naive Bayes.
- Produce a classification confidence score.

The ML Classifier classifies queries as benign or malicious.

---

## Threat Decision Engine

The Threat Decision Engine combines the outputs of the Rule Engine and ML Classifier.

Responsibilities

- Evaluate detection results.
- Calculate a unified security risk score.
- Determine the final enforcement action.

Possible decisions

- ALLOW
- BLOCK

The Threat Decision Engine is the only component authorized to make enforcement decisions.

---

## Response Engine

Responsibilities

- Execute Threat Decision Engine decisions.
- Forward approved queries.
- Reject blocked queries.
- Generate alerts.
- Trigger audit logging.

---

## Database

The PostgreSQL database stores application data.

All database communication uses parameterized queries.

Direct client access is prohibited.

---

## Audit Logging

Responsibilities

- Record authentication events.
- Record SQL queries.
- Record detection results.
- Record enforcement decisions.
- Record alerts.

Audit records are immutable.

---

## AI Prompt Guard

The Prompt Guard protects the AI explanation pipeline.

Responsibilities

- Sanitize AI inputs.
- Filter prompt injection attempts.
- Isolate AI prompts.
- Restrict AI context.

The Prompt Guard has no authority over security enforcement.

---

## AI Threat Explainer

Responsibilities

- Generate natural-language explanations.
- Explain why queries were blocked.
- Explain rule matches.
- Explain ML classification results.

The AI Threat Explainer is advisory only.

---

## Output Validator

Responsibilities

- Validate AI responses.
- Remove unsafe content.
- Ensure structured output.
- Prevent unsafe instructions from reaching users.

---

## Dashboard & Reports

Responsibilities

- Display live alerts.
- Display security events.
- Display audit logs.
- Display security risk scores.
- Display generated reports.

---

# 4. Request Flow

Every request follows the exact sequence below.

```
Client Request
        │
        ▼
Rate Limiter
        │
        ▼
JWT Authentication
        │
        ▼
RBAC Authorization
        │
        ▼
Pydantic Validation
        │
        ▼
Gateway Layer

Interceptor
        │
Canonicalizer
        │
Tokenizer
        │
Feature Extractor
        │
        ▼

Detection Layer

Rule Engine
        │
ML Classifier
        │
        ▼

Threat Decision Engine
        │
        ▼

Response Engine

├── ALLOW
│       │
│       ▼
│   Audit Log
│       │
│       ▼
│ PostgreSQL
│
└── BLOCK
        │
        ▼
    Audit Log
        │
        ▼
   Alert Service
        │
        ▼
 AI Prompt Guard
        │
        ▼
AI Threat Explainer
        │
        ▼
Output Validator
        │
        ▼
Dashboard & Reports
```

No component may bypass this pipeline.

---

# 5. Security Architecture

## Layer 1 — Network Protection

- HTTPS
- CORS
- Rate Limiting

---

## Layer 2 — Authentication

- JWT Authentication
- Password Hashing (bcrypt)

---

## Layer 3 — Authorization

- Role-Based Access Control
- Permission Validation

---

## Layer 4 — Input Validation

- Pydantic Validation
- Type Validation
- Length Validation

---

## Layer 5 — Threat Detection

- Rule Engine
- TF-IDF Feature Extraction
- Multinomial Naive Bayes Classification

---

## Layer 6 — Decision Making

- Threat Decision Engine
- Deterministic Enforcement

---

## Layer 7 — Database Protection

- Parameterized Queries
- Least-Privilege Access
- Audit Logging

---

## Layer 8 — AI Protection

- Prompt Guard
- Output Validation

---

# 6. Component Responsibilities

| Component | Responsibility |
|------------|----------------|
| Rate Limiter | Control request rate |
| Authentication | Verify identity |
| Authorization | Verify permissions |
| Validation | Validate requests |
| Interceptor | Capture SQL queries |
| Canonicalizer | Normalize SQL |
| Tokenizer | Tokenize SQL |
| Feature Extractor | Extract ML features |
| Rule Engine | Detect SQL Injection |
| ML Classifier | Classify SQL queries |
| Threat Decision Engine | Generate security decisions |
| Response Engine | Execute enforcement |
| Database | Store application data |
| Audit Logging | Record security events |
| AI Prompt Guard | Protect AI inputs |
| AI Threat Explainer | Explain security decisions |
| Output Validator | Validate AI responses |
| Dashboard | Display security information |

Each component has exactly one responsibility.

---

# 7. Engineering Constraints

SentinelSQL intentionally excludes:

- Dynamic SQL execution
- Multi-statement SQL
- Direct database access
- AI-generated SQL
- AI-controlled security decisions
- Hardcoded credentials
- Raw SQL string concatenation

---

# 8. Design Principles

SentinelSQL follows these engineering principles.

- Security before convenience.
- Zero Trust by default.
- Defense in Depth.
- Secure by Default.
- Single Responsibility Principle.
- Explainable Security.
- Least Privilege.
- Deterministic Enforcement.
- Modular Design.

---

# 9. Future Extensions

The architecture supports future expansion without redesign.

Potential extensions include:

- Additional database engines
- Additional machine-learning classifiers
- Threat intelligence integration
- Multi-LLM support
- Docker deployment
- Kubernetes deployment
- Cloud deployment
- SIEM integration

These capabilities are outside the MVP scope.

---

# 10. Architecture Freeze

This document defines the official SentinelSQL software architecture.

All implementation must conform to this architecture.

Architectural changes require explicit approval before implementation.

No implementation may silently alter this architecture.