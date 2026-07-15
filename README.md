# Automated PRD-to-API Specification Generator

An end-to-end recursive AI workflow built in Google AI Studio that transforms a raw product idea into production-ready software architecture artifacts.

The workflow progressively converts a simple product idea into a structured Product Requirements Document (PRD), a normalized database schema, backend domain models, a REST API specification, and finally validates the entire architecture for consistency and completeness.

---

## Project Overview

Modern software projects often require multiple artifacts before development can begin:

- Product Requirements Document (PRD)
- Database Schema
- Backend Models
- REST API Specification
- Architecture Validation

Instead of creating these manually, this project demonstrates how a multi-stage AI workflow can automate the process.

Each stage consumes the output of the previous stage, creating a recursive pipeline that maintains consistency from business requirements to implementation-ready specifications.

---

## Workflow

```text
Raw Product Idea
        │
        ▼
Stage 1 – Product Requirements Document (PRD)
        │
        ▼
Stage 2 – Database Schema & Domain Events
        │
        ▼
Stage 3 – Backend Models
        │
        ▼
Stage 4 – REST API Specification (OpenAPI)
        │
        ▼
Stage 5 – Architecture Validation
```

Each stage is independent but uses the previous stage as its input.

---

# Repository Structure

```
automated-prd-api-generator/
│
├── README.md
│
├── prompts/
│   ├── stage1_system_prompt.md
│   ├── stage1_prd_prompt.md
│   ├── stage2_system_prompt.md
│   ├── stage2_database_prompt.md
│   ├── stage3_system_prompt.md
│   ├── stage3_models_prompt.md
│   ├── stage4_system_prompt.md
│   ├── stage4_api_prompt.md
│   ├── stage5_system_prompt.md
│   └── stage5_validation_prompt.md
│
├── inputs/
│   └── finance_app.txt
│
├── outputs/
│   ├── finance_prd.json
│   ├── finance_schema.json
│   ├── backend_models.json
│   ├── openapi_spec.json
│   └── validation_report.json
│
└── diagrams/
```

---

# Example Input

```
A fintech app that alerts users whenever any stock in their portfolio drops by a customizable percentage.

Users connect their brokerage accounts.

The application continuously monitors stock prices.

Push notifications are sent immediately whenever thresholds are reached.

Users can configure different thresholds for different stocks.
```

---

# Stage 1 – Product Requirements Document

Purpose:

Transform a raw product idea into a structured JSON Product Requirements Document.

Output includes:

- Product overview
- Problem statement
- Target users
- Actors
- Core features
- User stories
- Business rules
- Key entities
- Lifecycle states
- Edge cases
- Success metrics
- Technical considerations

Output File

```
outputs/finance_prd.json
```

---

# Stage 2 – Database Schema

Purpose:

Convert the PRD into a normalized PostgreSQL database design.

Output includes:

- Tables
- Columns
- Relationships
- Junction tables
- Constraints
- Indexes
- Enums
- Domain events
- Webhook events

Output File

```
outputs/finance_schema.json
```

---

# Stage 3 – Backend Models

Purpose:

Generate backend architecture from the database schema.

Output includes:

- Domain models
- DTOs
- Repository interfaces
- Service interfaces
- Aggregate roots
- Validation rules

Output File

```
outputs/backend_models.json
```

---

# Stage 4 – REST API Specification

Purpose:

Generate an OpenAPI-ready REST API specification.

Output includes:

- Resources
- Endpoints
- Request DTOs
- Response DTOs
- Authentication
- Error responses
- Webhooks
- API versioning

Output File

```
outputs/openapi_spec.json
```

---

# Stage 5 – Architecture Validation

Purpose:

Validate the consistency of all previous stages.

Validation includes:

- Entity traceability
- Relationship consistency
- Business rule preservation
- Lifecycle validation
- API coverage
- Event consistency
- Webhook consistency

Output File

```
outputs/validation_report.json
```

---

# Technologies Used

- Google AI Studio (Gemini)
- Prompt Engineering
- JSON
- PostgreSQL Schema Design
- REST API Design
- OpenAPI Specification
- Git
- GitHub

---

# Key Concepts Demonstrated

- Recursive Prompt Engineering
- Systems Thinking
- Product Management
- Database Design
- API Design
- Domain-Driven Design (DDD)
- Event-Driven Architecture
- AI Workflow Validation

---

# Learning Outcomes

This project demonstrates how AI can be orchestrated across multiple stages to progressively transform a simple business idea into structured engineering artifacts while maintaining traceability and consistency.

Rather than producing a single response, each stage feeds the next, creating a recursive workflow that mirrors a real-world software design process.

---

# Future Improvements

- GraphQL API generation
- Frontend UI schema generation
- Infrastructure-as-Code generation
- CI/CD pipeline generation
- Test case generation
- Sequence diagrams
- Kubernetes deployment manifests

---

# Author

**Vera Ogbonna**

Product Manager | AI Product Management | Product Strategy

LinkedIn:
https://www.linkedin.com/in/vera-ogbonna

Email:
veraogbonna1@gmail.com

---
