# SentinelSQL Engineering Principles

**Version:** 1.0 (MVP)  
**Status:** Design Freeze

---

# 1. Purpose

This document defines the engineering principles governing the design, implementation, testing, and maintenance of SentinelSQL.

These principles are derived exclusively from the approved Product Specification, Software Architecture, Database Schema, API Contract, and Folder Structure.

Every implementation decision must conform to these principles.

---

# 2. Engineering Objectives

SentinelSQL is developed with three primary objectives:

- Usability
- Information Security & Integrity
- Efficient MVP Delivery

Every engineering decision should improve at least one objective without compromising the others.

---

# 3. Guiding Principles

SentinelSQL follows these core engineering principles.

- Security before convenience.
- Zero Trust by default.
- Defense in Depth.
- Least Privilege.
- Secure by Default.
- Deterministic Enforcement.
- Explainable Security.
- Single Responsibility Principle.
- Separation of Concerns.
- Modular Design.
- Maintainability over complexity.
- Simplicity over unnecessary abstraction.

---

# 4. Security Principles

Every request must satisfy the complete security pipeline.

```

Client Request

↓

Rate Limiter

↓

JWT Authentication

↓

RBAC Authorization

↓

Pydantic Validation

↓

SQL Gateway

↓

Detection Layer

↓

Threat Decision Engine

↓

Response Engine

```

No component may bypass any security layer.

---

# 5. Authentication Principles

- Every protected endpoint requires JWT authentication.
- User identity must be verified before business logic executes.
- Passwords are stored only as bcrypt hashes.
- Authentication failures immediately terminate request processing.

---

# 6. Authorization Principles

- Every authenticated request must undergo RBAC authorization.
- Authorization occurs before business logic.
- Access is granted according to assigned user roles.
- Unauthorized requests are rejected immediately.

---

# 7. Validation Principles

All external input is considered untrusted.

Every request must be validated using Pydantic models before processing.

Validation includes:

- Required fields
- Data types
- Input structure
- Length constraints

Malformed requests must never reach business logic.

---

# 8. SQL Processing Principles

Every SQL query must pass through the SQL Gateway.

Processing order:

1. Interception
2. Canonicalization
3. Tokenization
4. Feature Extraction
5. Detection
6. Threat Decision
7. Response

No SQL query may reach PostgreSQL before completing this pipeline.

---

# 9. Detection Principles

The Detection Layer consists of two independent components.

## Rule Engine

Responsibilities

- Detect known SQL Injection patterns.
- Apply deterministic detection rules.

## ML Classifier

Responsibilities

- Generate TF-IDF feature vectors.
- Classify SQL queries using Multinomial Naive Bayes.

Neither component performs enforcement.

---

# 10. Decision Principles

The Threat Decision Engine is the only component authorized to determine enforcement actions.

Possible decisions:

- ALLOW
- BLOCK

No other component may override, modify, or bypass these decisions.

---

# 11. AI Principles

The AI subsystem exists solely to explain security decisions.

AI responsibilities include:

- Explain detections.
- Explain blocked queries.
- Generate incident summaries.

The AI subsystem must never:

- Execute SQL.
- Access PostgreSQL directly.
- Modify enforcement decisions.
- Override the Threat Decision Engine.
- Perform autonomous security actions.

AI is advisory only.

---

# 12. Prompt Injection Principles

Every AI request must pass through the AI Prompt Guard.

The Prompt Guard is responsible for:

- Input sanitization.
- Prompt isolation.
- Context restriction.

Every AI response must pass through the Output Validator before being returned.

---

# 13. Database Principles

PostgreSQL is the only supported database for the MVP.

Database access principles:

- Parameterized queries only.
- Least-privilege access.
- Referential integrity.
- UUID primary keys.
- Immutable audit logs.

Direct database access from the client is prohibited.

---

# 14. API Principles

The API follows these rules:

- HTTPS only.
- JSON request/response format.
- Stateless communication.
- Consistent HTTP status codes.
- Deterministic behavior.

Protected endpoints require:

- JWT Authentication
- RBAC Authorization
- Request Validation

---

# 15. Code Organization Principles

Each module has exactly one responsibility.

Responsibilities must not overlap.

Business logic must remain independent from:

- API routing
- Authentication
- Database configuration
- Frontend components

Reusable functionality belongs in dedicated services or utility modules.

---

# 16. Logging Principles

Every security-relevant action must be recorded.

Audit logging includes:

- Authentication events
- SQL query processing
- Detection results
- Enforcement decisions
- Incident creation
- AI explanation generation

Audit records are append-only.

---

# 17. Error Handling Principles

Errors must:

- Fail safely.
- Return appropriate HTTP status codes.
- Never expose sensitive information.
- Never reveal internal implementation details.
- Be recorded when security relevant.

---

# 18. Development Principles

Implementation must:

- Follow the approved Product Specification.
- Follow the approved Software Architecture.
- Follow the approved Database Schema.
- Follow the approved API Contract.
- Follow the approved Folder Structure.

Implementation must not introduce undocumented behavior.

---

# 19. Scope Control

The MVP intentionally excludes:

- Production deployment
- Cloud infrastructure
- Multi-tenant architecture
- WAF functionality
- SIEM integration
- AI-controlled security decisions
- Additional database engines

No implementation may introduce these capabilities without explicit approval.

---

# 20. Change Management

The following documents are the governing design authority:

- product_specification.md
- architecture.md
- database_schema.md
- api_contract.md
- folder_structure.md
- engineering_principles.md

If implementation conflicts with these documents:

- Implementation must be corrected.
- The documents remain authoritative.

Changes to these documents require explicit approval before implementation proceeds.

---

# 21. Engineering Freeze

This document establishes the engineering standards for SentinelSQL MVP.

All implementation must conform to these principles.

No architectural, security, or functional deviation is permitted without prior approval.