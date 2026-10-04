# IDP — Internal Developer Platform

## One-line description
A CLI-first Internal Developer Platform providing secure, idempotent, and auditable deployment workflows.

## Product overview
The IDP provides a paved path for developers to deploy applications with built-in security, observability, and point-in-time correctness. It enforces strict RBAC, separates synchronous API requests from privileged asynchronous execution, and includes an ML-driven advisory layer for predicting deployment failures.

## Problem statement
Developers need a reliable and secure way to deploy applications without interacting directly with privileged environments like Docker sockets. The IDP solves this by introducing a gateway-worker architecture that guarantees security boundaries, idempotency, and full auditability.

## Target users
Internal developers and engineering teams requiring standardized, secure deployment workflows.

## Planned capabilities
**IMPLEMENTED**
- Foundation, project blueprint, and architectural boundaries (PR 01).
- 100-PR Execution Strategy and CI foundation.

**PLANNED**
- Authentication & RBAC via Gateway.
- Durable state management (PostgreSQL).
- Idempotency & temporary state (Redis).
- Asynchronous execution (Queue & Worker).
- Privileged deployment boundary (Docker Socket Proxy).
- Webhook Ingestion & Deduplication.
- ML-based failure prediction.
- Comprehensive Observability Stack (OpenTelemetry, Prometheus, Grafana, Jaeger).

## High-level architecture
The IDP follows a strict boundary model:
`Developer/CLI → Gateway → Queue → Worker → Docker Socket Proxy → Docker`
The Gateway handles authentication and authorization. The Worker handles privileged execution. A PostgreSQL database maintains the source of truth, while Redis handles caching and idempotency. An advisory ML pipeline predicts deployment risks based on GitHub events.

## Security philosophy
Security is enforced through isolation and least privilege. The public-facing Gateway has no direct access to the execution environment (Docker). Privileged actions are executed by an isolated Worker and must be fully auditable. Secrets are strictly managed and webhook payloads are cryptographically verified.

## Development strategy
The project is being developed through exactly 100 PRs to ensure architectural clarity, incremental implementation, and strict scope control.

## Current status
**PR 01 / 100**
This PR establishes the architectural blueprint, repository foundation, security boundaries, and CI quality gates required for the remaining 99 PRs.

## Testing
The testing strategy includes unit tests, integration tests, API validation, security boundary tests, and chaos testing (e.g., worker termination recovery).

## CI
A GitHub Actions workflow establishes the CI quality gate, enforcing formatting, linting, type checking, and test execution. 

## Observability
The platform will utilize structured logging, distributed tracing (OpenTelemetry), metrics collection (Prometheus), and dashboards (Grafana, Jaeger) to provide full visibility into deployment workflows.

## Development instructions
*Note: Development commands will be introduced in future PRs as the capabilities are implemented.*
