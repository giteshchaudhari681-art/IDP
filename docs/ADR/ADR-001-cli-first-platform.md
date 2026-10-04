# ADR 001: CLI-First Platform

## Status
Accepted

## Context
Developers need a paved path to deploy applications without interacting with complex underlying infrastructure (e.g., Kubernetes, direct Docker commands). A UI dashboard is useful for observability but slows down the active deployment and feedback loop.

## Decision
The Internal Developer Platform (IDP) will be built as a CLI-first platform. All core developer workflows (deployment, status checks, logs) must be primarily accessible and fully functional via a CLI tool.

## Consequences
- Requires designing a robust CLI with clear UX.
- Synchronous feedback must be provided for API interactions.
- Dashboards are secondary and reserved for deep observability, not primary deployment actions.

## Alternatives considered
- **Dashboard-first:** Rejected because it interrupts the developer's terminal-based workflow.
- **GitOps-only (no CLI):** Rejected because it lacks immediate synchronous validation of user intent before committing.
