# Architecture

This document describes the high-level architecture of the IDP. *Note: This represents the final intended architecture. Actual implementation will occur progressively across the 100-PR roadmap.*

## CLI
**Future Responsibility:** The primary developer-facing interface.

## Gateway
**Future Responsibility:** Handles authentication, authorization, RBAC, rate limiting, idempotency, and API orchestration. 
*Important:* The Gateway must NOT have Docker Engine/socket access.

## PostgreSQL
**Future Responsibility:** The durable source of truth. It will manage users, teams, memberships, services, build events, deployments, audit records, and refresh tokens.

## Redis
**Future Responsibility:** Handles webhook deduplication, rate limiting, idempotency, and temporary cache/state.

## Queue
**Future Responsibility:** Separates synchronous API requests from asynchronous processing.

## Worker
**Future Responsibility:** Privileged deployment execution. The Worker is the only component allowed to interact with Docker.

## Docker Socket Proxy
**Future Responsibility:** Restricts Docker Engine API capabilities to provide an additional layer of isolation.

## Webhook Ingestion
**Future Responsibility:** Receives GitHub events, verifies signatures, deduplicates deliveries, normalizes events, and enqueues processing.

## Prediction Service
**Future Responsibility:** Handles feature extraction, model inference, evaluation, and prediction API for deployment failure risks.

## Observability
**Future Responsibility:** Collects, processes, and displays system metrics, structured logs, and distributed traces using OpenTelemetry, Prometheus, Grafana, and Jaeger.

## Security Boundary
The following architectural boundary is mandatory:
`Internet / Developer → Gateway → Queue → Worker → Docker Socket Proxy → Docker`

The public Gateway MUST NOT have direct Docker access. The Worker is the privileged execution boundary. The socket proxy provides additional restriction. This is an architectural invariant.
