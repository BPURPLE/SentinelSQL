# SentinelSQL Roadmap

**Version:** 1.0 (MVP)  
**Status:** Design Freeze

---

# 1. Purpose

This document defines the official development roadmap for the SentinelSQL MVP.

The roadmap translates the approved Product Specification, Software Architecture, Database Schema, API Contract, Folder Structure, and Engineering Principles into an implementation sequence.

This roadmap does not introduce new features or alter the approved project scope.

---

# 2. Development Objectives

The implementation follows three primary objectives:

- Deliver a secure MVP within the project timeline.
- Preserve the integrity of the approved architecture.
- Maintain a modular, maintainable, and testable codebase.

---

# 3. Development Phases

| Phase | Goal | Status |
|--------|------|--------|
| Phase 1 | Documentation Freeze | Complete |
| Phase 2 | Repository Setup | Pending |
| Phase 3 | Backend Foundation | Pending |
| Phase 4 | Authentication & Authorization | Pending |
| Phase 5 | SQL Gateway | Pending |
| Phase 6 | Detection Layer | Pending |
| Phase 7 | Threat Decision & Response | Pending |
| Phase 8 | AI Explanation Pipeline | Pending |
| Phase 9 | Dashboard | Pending |
| Phase 10 | Testing & Finalization | Pending |

---

# 4. Phase 1 — Documentation Freeze

Objective

Freeze all project documentation before implementation.

Deliverables

- product_specification.md
- architecture.md
- database_schema.md
- api_contract.md
- folder_structure.md
- engineering_principles.md
- roadmap.md

Completion Criteria

- All documentation is internally consistent.
- No architectural conflicts exist.
- Documentation is committed to version control.

---

# 5. Phase 2 — Repository Setup

Objective

Prepare the repository for implementation.

Deliverables

- Repository structure
- Backend directory
- Frontend directory
- Documentation directory
- Test directory
- Docker directory
- GitHub workflow directory

Completion Criteria

- Repository matches folder_structure.md.
- All placeholder files exist.
- Initial documentation commit completed.

---

# 6. Phase 3 — Backend Foundation

Objective

Create the backend application foundation.

Deliverables

- FastAPI application
- Application configuration
- Database connection
- Project configuration
- Shared schemas
- Shared utilities

Completion Criteria

- Backend starts successfully.
- Configuration loads correctly.
- Database connection established.

---

# 7. Phase 4 — Authentication & Authorization

Objective

Implement secure access control.

Deliverables

- JWT Authentication
- Password hashing
- RBAC Authorization
- Protected endpoints

Completion Criteria

- Authenticated users receive JWT tokens.
- Protected endpoints require authentication.
- RBAC enforcement operational.

---

# 8. Phase 5 — SQL Gateway

Objective

Implement the SQL Gateway pipeline.

Deliverables

- SQL Interceptor
- Canonicalizer
- Tokenizer
- Feature Extractor

Completion Criteria

- Every SQL query passes through the complete gateway.
- Query metadata generated successfully.

---

# 9. Phase 6 — Detection Layer

Objective

Implement SQL threat detection.

Deliverables

- Rule Engine
- TF-IDF Feature Extraction
- Multinomial Naive Bayes Classifier

Completion Criteria

- Rule-based detection operational.
- ML classifier operational.
- Detection results generated for every query.

---

# 10. Phase 7 — Threat Decision & Response

Objective

Implement deterministic enforcement.

Deliverables

- Threat Decision Engine
- Response Engine
- Audit Logging
- Incident Generation

Completion Criteria

- Every query receives a decision.
- ALLOW requests reach PostgreSQL.
- BLOCK requests are rejected.
- Audit logs created.

---

# 11. Phase 8 — AI Explanation Pipeline

Objective

Implement secure AI-assisted explanations.

Deliverables

- AI Prompt Guard
- AI Threat Explainer
- Output Validator

Completion Criteria

- AI explanations generated for incidents.
- Prompt Guard active.
- Output validation operational.
- AI remains advisory only.

---

# 12. Phase 9 — Dashboard

Objective

Implement visualization.

Deliverables

- Dashboard
- Incident Viewer
- Audit Log Viewer
- Security Reports

Completion Criteria

- Dashboard displays system activity.
- Incident information available.
- Reports generated successfully.

---

# 13. Phase 10 — Testing & Finalization

Objective

Validate the complete MVP.

Deliverables

- Unit Tests
- Integration Tests
- End-to-End Tests
- Documentation Review
- Final Demonstration

Completion Criteria

- Authentication validated.
- Gateway validated.
- Detection validated.
- Decision Engine validated.
- AI pipeline validated.
- Dashboard validated.

---

# 14. Implementation Order

Implementation must follow this sequence.

1. Backend Foundation
2. Authentication
3. Authorization
4. Validation
5. SQL Gateway
6. Rule Engine
7. ML Classifier
8. Threat Decision Engine
9. Response Engine
10. Database Integration
11. Audit Logging
12. AI Prompt Guard
13. AI Threat Explainer
14. Output Validator
15. Dashboard
16. Testing

Implementation must not skip dependencies.

---

# 15. Milestones

| Milestone | Deliverable |
|------------|-------------|
| M1 | Documentation Freeze |
| M2 | Repository Ready |
| M3 | Backend Operational |
| M4 | Secure Authentication Complete |
| M5 | SQL Gateway Complete |
| M6 | Detection Layer Complete |
| M7 | Threat Decision Pipeline Complete |
| M8 | AI Explanation Pipeline Complete |
| M9 | Dashboard Complete |
| M10 | MVP Complete |

---

# 16. Definition of Done

The SentinelSQL MVP is complete when:

- The implementation conforms to all approved documentation.
- All protected endpoints enforce JWT authentication and RBAC.
- Every SQL query passes through the SQL Gateway.
- Rule-based detection is operational.
- TF-IDF + Multinomial Naive Bayes classification is operational.
- The Threat Decision Engine generates deterministic ALLOW or BLOCK decisions.
- Approved queries reach PostgreSQL.
- Blocked queries generate incidents and audit logs.
- AI explanations are generated through the Prompt Guard and Output Validator.
- The dashboard displays incidents and security events.
- The project satisfies the Product Specification, Software Architecture, Database Schema, API Contract, Folder Structure, and Engineering Principles.

---

# 17. Roadmap Freeze

This roadmap defines the official implementation sequence for the SentinelSQL MVP.

Development must follow this roadmap unless the governing design documents are explicitly updated and approved.

No implementation may introduce functionality outside the approved MVP scope.