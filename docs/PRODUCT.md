# Product Definition

## Product Vision
To provide a secure, idempotent, and predictable CLI-first Internal Developer Platform that allows engineering teams to deploy applications reliably without compromising the security boundaries of the underlying infrastructure.

## Problem Statement
Deployments that rely on direct interaction with privileged systems (like Docker sockets) create unacceptable security risks, lack auditability, and introduce failure states when asynchronous jobs fail. The IDP solves this by creating a structured gateway-worker boundary.

## Target Users
Internal developers, operations teams, and platform engineers.

## Developer Experience
The platform is designed to be CLI-first, providing immediate synchronous feedback for API interactions while securely orchestrating asynchronous background deployment tasks.

## Core Workflows
*Note: This is an architectural description. Implementation belongs to future PRs.*
- **Deployment:** Developer CLI → Gateway → Queue → Worker → Docker Proxy → Docker.
- **Webhook Ingestion:** GitHub Webhook → Verification → Deduplication → Queue → ML Prediction.

## Product Capabilities
**Current implementation:**
- Project Foundation and Architectural Blueprint.

**Future capability:**
- CLI interaction.
- Secure API Gateway.
- Worker-based execution.
- ML-driven deployment failure prediction.
- Observability and Tracing.

## Non-Goals
- Replacing general-purpose orchestrators like Kubernetes.
- Supporting unregulated direct access to execution environments.

## Reliability Expectations
The IDP must survive component failures. Workers must be able to resume or cleanly fail deployments if they crash during execution.

## Security Expectations
Total isolation between the public-facing Gateway and the privileged Worker. Zero trust across the API boundary. Complete auditability of state changes.

## ML Expectations
The ML system predicting deployment failure must be purely advisory and non-load-bearing. It cannot block deployments if the ML service is unavailable.

## Observability Expectations
Comprehensive tracing from the CLI request to the final container deployment using OpenTelemetry.

## Future Scope
This document outlines the product vision. The actual implementation of the Gateway, Worker, CLI, ML, and underlying infrastructure will occur sequentially over the 100-PR roadmap.
