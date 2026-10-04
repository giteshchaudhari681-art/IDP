# ADR 002: Gateway-Worker Separation

## Status
Accepted

## Context
Deployments involve privileged operations (e.g., interacting with container runtimes). Exposing an API that directly orchestrates these operations creates a significant security risk. If the API is compromised, the entire infrastructure is compromised. Furthermore, deployment tasks are long-running and asynchronous.

## Decision
We will strictly separate the Gateway from the Worker. The Gateway will handle synchronous API requests, authentication, and authorization. The Worker will handle privileged asynchronous execution. They will communicate via a Queue.

## Consequences
- The Gateway will have zero access to the execution environment.
- Asynchronous task processing is mandatory.
- We must handle eventual consistency and task idempotency.

## Alternatives considered
- **Monolithic API:** Rejected due to security risks and the danger of blocking synchronous threads on long-running tasks.
