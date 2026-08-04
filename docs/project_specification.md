# SentinelSQL Product Specification

**Version:** 1.0 (MVP)  
**Status:** Design Freeze

---

# 1. Product Overview

SentinelSQL is an AI-assisted database security gateway that intercepts SQL queries before execution, detects malicious database activity using rule-based analysis and machine learning, and provides explainable security insights through a secure AI explanation pipeline.

The MVP operates in a controlled environment using a sample CRUD application connected to a sandboxed PostgreSQL database. Every SQL query is inspected before execution, assigned a risk assessment, and either allowed or blocked according to deterministic security policies.

The AI subsystem is advisory only and never participates in security enforcement.

---

# 2. Problem Statement

Most web applications rely primarily on application-layer validation to protect their databases. Vulnerabilities such as SQL Injection, malicious query manipulation, and unauthorized database activity may still bypass these protections.

SentinelSQL introduces an independent database security layer positioned between the application and the database. Every SQL query passes through SentinelSQL before execution, allowing the system to inspect, classify, evaluate, and respond to suspicious activity in real time.

---

# 3. Target Users

## Primary Users

- Students
- Developers
- Security Researchers

## Secondary Users

- Cybersecurity Educators
- Academic Institutions
- Small Engineering Teams

---

# 4. Objectives

The SentinelSQL MVP aims to:

- Authenticate every incoming request.
- Authorize requests using Role-Based Access Control (RBAC).
- Monitor every SQL query before database execution.
- Canonicalize and extract features from SQL queries.
- Detect known SQL Injection attacks using rule-based analysis.
- Classify SQL queries as benign or malicious using machine learning.
- Combine detection results into a deterministic security decision.
- Calculate a unified risk assessment for every query.
- Generate explainable security alerts and reports.
- Maintain immutable audit logs.
- Visualize security events through a real-time dashboard.
- Provide secure AI-assisted threat explanations.
- Protect the AI explanation pipeline from prompt injection attacks.

---

# 5. MVP Scope

## Included

- JWT Authentication
- Role-Based Access Control (RBAC)
- SQL Query Monitoring
- SQL Canonicalization
- SQL Tokenization
- Feature Extraction
- Rule-Based SQL Injection Detection
- TF-IDF Feature Vectorization
- Multinomial Naive Bayes Classification
- Threat Decision Engine
- Risk Assessment
- Audit Logging
- Incident Dashboard
- AI Threat Explanation
- AI Prompt Guard
- Security Report Generation

## Excluded

- Production Deployment
- Multi-Tenant Architecture
- Cloud Infrastructure
- Network Packet Inspection
- Web Application Firewall (WAF)
- SIEM Integration
- Active Directory / LDAP
- Enterprise Compliance
- Distributed Detection
- Cross-Database Clustering

---

# 6. Functional Requirements

| ID | Requirement |
|----|-------------|
| FR-01 | User Authentication |
| FR-02 | Role-Based Authorization (RBAC) |
| FR-03 | SQL Query Monitoring |
| FR-04 | SQL Canonicalization, Tokenization & Feature Extraction |
| FR-05 | Rule-Based SQL Injection Detection |
| FR-06 | SQL Query Classification (TF-IDF + Multinomial Naive Bayes) |
| FR-07 | Threat Decision Engine |
| FR-08 | Risk Assessment |
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
- Enforce RBAC authorization.
- Process CRUD database requests.
- Inspect every SQL query before execution.
- Detect common SQL Injection attacks.
- Correctly classify SQL queries as benign or malicious using machine learning.
- Generate deterministic security decisions.
- Block or allow queries according to the Threat Decision Engine.
- Record complete audit logs.
- Generate explainable AI-assisted threat summaries.
- Successfully mitigate a documented prompt injection evaluation suite.
- Display incidents on a real-time dashboard.
- Generate security reports.

---

# 9. Future Roadmap

## Security

- Production Database Proxy
- MySQL Support
- Microsoft SQL Server Support
- Oracle Database Support
- Advanced SQL Classification
- Threat Intelligence Integration
- SIEM Integration

## Artificial Intelligence

- Advanced Prompt Injection Detection
- Multi-LLM Support
- Retrieval-Augmented Generation (RAG)
- AI-Assisted Rule Generation

## Platform

- Docker Deployment
- Kubernetes
- Cloud Deployment
- Multi-Tenant Architecture

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
- TF-IDF Vectorizer
- Multinomial Naive Bayes

## Authentication

- JWT
- bcrypt

## Validation

- Pydantic

## Visualization

- Recharts

## Version Control

- Git
- GitHub

## AI Development

- Codex
- CodeRabbit

---

# 11. Guiding Principles

SentinelSQL follows these engineering principles:

- Security before convenience.
- Zero Trust by default.
- Every request is authenticated.
- Every request is authorized.
- Every SQL query is inspected before execution.
- Every security decision is deterministic.
- AI explains decisions but never makes them.
- Prompt Guard protects the AI explanation pipeline.
- Every critical action is auditable.
- Components remain modular and independently testable.

---

# 12. MVP Constraints

To ensure successful delivery within the project timeline:

- PostgreSQL is the only supported database.
- Supported SQL operations are SELECT, INSERT, UPDATE and DELETE.
- Only single-statement SQL queries are supported.
- General-purpose SQL parsing is out of scope.
- Machine learning is trained using a labeled dataset of benign and malicious SQL queries.
- AI explanations are advisory only.
- AI never influences enforcement decisions.
- Security enforcement is performed exclusively by the Threat Decision Engine.

---

# 13. Architecture Principles

SentinelSQL follows a layered security architecture.

Client Request

↓

Rate Limiter

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

ML Classifier (TF-IDF + Multinomial Naive Bayes)

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

The Threat Decision Engine is the only component authorized to determine security enforcement.

The AI subsystem may explain security decisions but can never modify, override, or generate them.s