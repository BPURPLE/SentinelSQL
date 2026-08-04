# SentinelSQL API Contract

**Version:** 1.0 (MVP)  
**Status:** Design Freeze

---

# 1. Purpose

This document defines the public REST API exposed by SentinelSQL.

The API provides secure access to authentication, SQL query inspection, incident monitoring, audit records, AI-generated explanations, and dashboard data.

This API contract is derived exclusively from the approved Product Specification, Software Architecture, and Database Schema.

No endpoint defined here may bypass the security architecture.

---

# 2. API Principles

The SentinelSQL API follows these principles:

- HTTPS only.
- JWT authentication required unless explicitly stated.
- Role-Based Access Control enforced on every protected endpoint.
- All request bodies validated using Pydantic models.
- JSON request and response format.
- Stateless communication.
- Deterministic server behavior.
- AI responses are advisory only.

---

# 3. Authentication

Protected endpoints require:

```

Authorization: Bearer \<JWT>

```

Requests without a valid JWT must be rejected.

---

# 4. API Endpoints

---

## Authentication

### POST /api/v1/auth/login

Authenticates a user and returns a JWT.

Authentication Required

- No

Request

```json
{
  "username": "string",
  "password": "string"
}
```

Response

```json
{
  "access_token": "jwt",
  "token_type": "Bearer"
}
```

---

### GET /api/v1/auth/me

Returns information about the authenticated user.

Authentication Required

- Yes

Response

```json
{
  "id": "uuid",
  "username": "string",
  "email": "string",
  "role": "string"
}
```

---

## SQL Gateway

### POST /api/v1/query/analyze

Submits a SQL query to the SentinelSQL security pipeline.

Authentication Required

- Yes

Request

```json
{
  "query": "SELECT * FROM users WHERE id = 1;"
}
```

Response

```json
{
  "query_id": "uuid",
  "decision": "ALLOW",
  "risk_score": 12
}
```

Possible Decisions

- ALLOW
- BLOCK

---

## Incidents

### GET /api/v1/incidents

Returns recorded incidents.

Authentication Required

- Yes

Response

```json
[
  {
    "incident_id": "uuid",
    "action": "BLOCK",
    "risk_score": 91,
    "created_at": "timestamp"
  }
]
```

---

### GET /api/v1/incidents/{incident_id}

Returns details for a single incident.

Authentication Required

- Yes

Response

```json
{
  "incident_id": "uuid",
  "query_id": "uuid",
  "action": "BLOCK",
  "risk_score": 91,
  "created_at": "timestamp"
}
```

---

## Audit Logs

### GET /api/v1/audit

Returns immutable audit records.

Authentication Required

- Yes

Response

```json
[
  {
    "event_type": "QUERY_BLOCKED",
    "created_at": "timestamp"
  }
]
```

---

## AI Explanation

### GET /api/v1/explanations/{incident_id}

Returns the validated AI explanation for an incident.

Authentication Required

- Yes

Response

```json
{
  "incident_id": "uuid",
  "explanation": "string",
  "validated": true
}
```

---

## Dashboard

### GET /api/v1/dashboard

Returns dashboard summary information.

Authentication Required

- Yes

Response

```json
{
  "total_queries": 0,
  "blocked_queries": 0,
  "incidents": 0
}
```

---

# 5. Request Processing Pipeline

Every protected endpoint follows the same processing sequence.

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

Business Logic

↓

Response

```

No endpoint may bypass this sequence.

---

# 6. Authorization

Role-Based Access Control is enforced on every protected endpoint.

| Endpoint | Authentication | RBAC |
|-----------|---------------|------|
| POST /auth/login | No | No |
| GET /auth/me | Yes | Yes |
| POST /query/analyze | Yes | Yes |
| GET /incidents | Yes | Yes |
| GET /incidents/{id} | Yes | Yes |
| GET /audit | Yes | Yes |
| GET /explanations/{id} | Yes | Yes |
| GET /dashboard | Yes | Yes |

---

# 7. HTTP Status Codes

| Code | Meaning |
|------|---------|
| 200 | Success |
| 201 | Resource Created |
| 400 | Invalid Request |
| 401 | Authentication Failed |
| 403 | Permission Denied |
| 404 | Resource Not Found |
| 422 | Validation Failed |
| 500 | Internal Server Error |

---

# 8. Error Response Format

All errors use a consistent JSON structure.

Example

```json
{
  "detail": "Authentication failed."
}
```

---

# 9. Security Requirements

Every endpoint must enforce:

- HTTPS communication.
- JWT authentication where required.
- Role-Based Access Control.
- Pydantic request validation.
- Parameterized SQL queries.
- Immutable audit logging.
- AI Prompt Guard before AI explanation generation.
- Output validation before AI responses are returned.

---

# 10. API Constraints

The MVP intentionally limits the API.

- JSON requests only.
- JSON responses only.
- Stateless communication.
- Single SQL query per request.
- PostgreSQL only.
- CRUD SQL operations only.
- AI explanations are read-only.
- AI cannot execute SQL.
- AI cannot modify security decisions.

---

# 11. API Versioning

The SentinelSQL API uses URI versioning.

Current version

```

/api/v1/

```

Future versions must not modify the behavior of existing endpoints.

---

# 12. Contract Freeze

This document defines the official SentinelSQL API contract.

All backend implementation must conform to this contract.

API changes require explicit approval before implementation.