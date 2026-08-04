# SentinelSQL Product Specification

**Version:** 1.0 (MVP)  
**Status:** Design Freeze

---

# 1. Product Overview

SentinelSQL is an AI-assisted database security gateway that monitors SQL queries, detects malicious or anomalous database activity, and provides real-time alerts with explainable security insights.

The MVP is designed for controlled environments using a sample CRUD application connected to a sandboxed PostgreSQL database. It demonstrates how rule-based detection and behavioral anomaly detection can identify database threats before query execution while maintaining complete auditability and explainable incident reporting.

---

# 2. Problem Statement

Modern web applications primarily rely on application-layer validation to protect databases from attacks. However, vulnerabilities such as SQL Injection, privilege misuse, and abnormal database activity may still bypass these defenses.

SentinelSQL introduces an independent security layer positioned between the application and the database. Every database query passes through SentinelSQL before execution, allowing the system to inspect, evaluate, detect, and respond to suspicious activity in real time.

---

# 3. Target Users

## Primary Users

- Students
- Developers
- Security Researchers

## Secondary Users

- Cybersecurity Educators
- Small Engineering Teams
- Academic Institutions

---

# 4. Objectives

The SentinelSQL MVP aims to:

- Monitor all database queries passing through the security gateway.
- Detect known SQL Injection attacks using rule-based analysis.
- Detect abnormal query behavior using machine learning.
- Calculate a unified risk score for every query.
- Generate explainable security alerts and incident reports.
- Maintain immutable audit logs for all security events.
- Visualize database activity through a real-time dashboard.
- Provide secure AI-assisted threat explanations.
- Protect the AI explanation pipeline against prompt injection and malicious inputs.

---

# 5. MVP Scope

## Included

- User Authentication
- Role-Based Access Control (RBAC)
- SQL Query Monitoring
- SQL Query Canonicalization & Feature Extraction
- Rule-Based SQL Injection Detection
- Behavioral Anomaly Detection
- Threat Decision Engine
- Risk Scoring
- Audit Logging
- Incident Dashboard
- Security Report Generation
- AI Threat Explanation
- AI Prompt Guard

## Excluded

- Production Deployment
- Cloud Infrastructure
- Multi-Tenant Architecture
- Network Packet Inspection
- Web Application Firewall (WAF)
- SIEM Integration
- Active Directory / LDAP Integration
- Enterprise Compliance Modules
- Distributed Detection
- Cross-Database Clustering

---

# 6. Functional Requirements

| ID | Requirement |
|----|-------------|
| FR-01 | User Authentication |
| FR-02 | Role-Based Authorization (RBAC) |
| FR-03 | SQL Query Monitoring |
| FR-04 | SQL Query Canonicalization & Feature Extraction |
| FR-05 | Rule-Based SQL Injection Detection |
| FR-06 | Behavioral Anomaly Detection |
| FR-07 | Threat Decision Engine |
| FR-08 | Risk Score Generation |
| FR-09 | Incident Response & Alert Generation |
| FR-10 | Immutable Audit Logging |
| FR-11 | Dashboard Visualization |
| FR-12 | AI Threat Explanation |
| FR-13 | AI Prompt Guard |
| FR-14 | Security Report Generation |

---

# 7. Non-Functional Requirements

## Security

- HTTPS communication
- JWT Authentication
- Password Hashing (bcrypt)
- Role-Based Access Control
- Parameterized SQL Queries
- Least-Privilege Database Access
- Prompt Injection Mitigation
- AI Input Sanitization
- AI Output Validation

## Performance

- Low-latency request processing
- Efficient rule evaluation
- Lightweight ML inference
- Responsive dashboard updates

## Reliability

- Structured logging
- Graceful error handling
- Immutable audit records

## Maintainability

- Modular architecture
- Separation of concerns
- Fully typed APIs
- Consistent coding standards

## Scalability

- Independent security modules
- Pluggable detection engines
- Extensible rule engine

---

# 8. Success Criteria

The MVP is considered complete when it can:

- Authenticate users securely.
- Enforce role-based authorization.
- Process CRUD database requests.
- Inspect every SQL query before execution.
- Detect common SQL Injection attacks.
- Detect abnormal query behavior using machine learning.
- Calculate and assign risk scores.
- Block or alert on malicious queries according to the Decision Engine policy.
- Generate AI-assisted threat explanations.
- Successfully mitigate a documented prompt injection evaluation suite.
- Record complete audit logs.
- Display incidents on a real-time dashboard.
- Generate security reports.

---

# 9. Future Roadmap

## Security

- Production Database Proxy
- MySQL Support
- Microsoft SQL Server Support
- Oracle Database Support
- Advanced Behavioral Profiling
- Threat Intelligence Feed Integration
- SIEM Integration

## Artificial Intelligence

- Advanced Prompt Injection Detection
- Multi-LLM Support
- Retrieval-Augmented Threat Intelligence (RAG)
- AI-Assisted Rule Generation
- Automated Threat Classification

## Platform

- Docker Deployment
- Kubernetes Support
- Cloud Deployment
- Multi-Tenant Architecture
- Enterprise Policy Engine

---

# 10. Technology Stack

## Frontend

- React
- Vite
- TypeScript
- Tailwind CSS

## Backend

- FastAPI
- Python

## Database

- PostgreSQL

## Machine Learning

- scikit-learn
- Isolation Forest

## Authentication

- JWT
- bcrypt

## Data Validation

- Pydantic

## Visualization

- Recharts

## Version Control

- Git
- GitHub

## AI Development

- Codex (Implementation)
- CodeRabbit (Code Review)

---

# 11. Guiding Principles

SentinelSQL follows the following engineering principles:

- Security before convenience.
- Zero Trust by default.
- Every request is authenticated and authorized.
- Every query is inspected before execution.
- AI assists security analysts but never makes security decisions.
- The AI Prompt Guard protects the AI explanation pipeline from malicious inputs.
- Every security decision must be explainable.
- Every critical action must be auditable.
- Sensitive data is never hardcoded.
- Components must remain modular, testable, and maintainable.

---

# 12. MVP Constraints

To ensure successful delivery within the project timeline, the MVP intentionally limits its scope.

- Database support is limited to PostgreSQL.
- Supported SQL operations are SELECT, INSERT, UPDATE, and DELETE.
- Only single-statement queries are supported.
- General-purpose SQL parsing is out of scope.
- AI explanations are advisory only and never influence enforcement decisions.
- Machine learning is trained exclusively on synthetic role-based traffic generated within the sandbox environment.
- Security enforcement is deterministic and handled solely by the Threat Decision Engine.

---

# 13. Architecture Principles

SentinelSQL is designed around a layered security architecture.

Application
↓
Authentication
↓
Authorization
↓
Validation
↓
SQL Gateway
↓
Canonicalization
↓
Rule Engine
↓
Behavioral ML Engine
↓
Threat Decision Engine
↓
Response Engine
↓
AI Prompt Guard
↓
AI Threat Explainer
↓
Output Validator
↓
Dashboard & Reports

Each layer has a single responsibility and communicates only through well-defined interfaces.

The Threat Decision Engine is the only component authorized to determine enforcement actions.

The AI subsystem may explain security decisions but can never modify, override, or generate them.