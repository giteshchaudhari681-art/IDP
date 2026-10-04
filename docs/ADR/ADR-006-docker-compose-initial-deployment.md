# ADR 006: Docker Compose Initial Deployment

## Status
Accepted

## Context
For the initial development and local testing phases of the platform itself, we need a way to reliably spin up the entire IDP stack (Gateway, Worker, DB, Redis, etc.) without requiring a complex orchestrator like Kubernetes.

## Decision
We will use Docker Compose as the standard orchestration tool for local development and initial deployments of the platform.

## Consequences
- Simplifies onboarding for developers working on the IDP.
- Provides a straightforward way to define network boundaries (e.g., separating the Gateway network from the Worker/Docker Proxy network).

## Alternatives considered
- **Minikube/Kind:** Rejected for the initial phases due to unnecessary complexity; we want to focus on architectural boundaries first, not Kubernetes manifests.
