# ADR 003: Docker Access Isolation

## Status
Accepted

## Context
The Worker needs to deploy containers. Providing raw Docker socket access to the Worker gives it root-level control over the host, which is a massive privilege escalation risk if the Worker itself is compromised.

## Decision
We will use a Docker Socket Proxy between the Worker and the Docker Engine. The Proxy will restrict access to only the specific Docker API endpoints required for deployment (e.g., creating, starting, and inspecting containers).

## Consequences
- Increased security by enforcing least privilege on the Docker API.
- Adds an additional infrastructure component (the proxy).
- Requires careful configuration of allowed API paths.

## Alternatives considered
- **Direct Docker Socket Mount:** Rejected because it provides unrestricted access to the host.
- **Rootless Docker:** Considered, but a proxy provides fine-grained API-level restriction which is required even in rootless environments.
