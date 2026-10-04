# Security Strategy

This document outlines the security requirements and boundaries for the IDP. *Note: These requirements guide the future implementation.*

### Authentication
Identity must be cryptographically verified via Gateway before any request is processed.

### Authorization
Permissions must be explicitly checked for every action.

### RBAC
Users must only operate within authorized team/service boundaries as defined in the source of truth.

### Least Privilege
Each component receives the minimum privileges required to function.

### Secret Management
Secrets must never be committed to the repository and must be securely injected at runtime.

### Webhook Verification
GitHub webhook signatures (HMAC) must be verified to prevent forged events.

### Deduplication
Duplicate webhook deliveries must not create duplicate processing pipelines or cause side effects.

### Docker Isolation
The Gateway MUST NOT have direct Docker socket access. The privileged execution boundary stops at the Worker.

### Auditability
All privileged actions must be recorded securely and auditable.

### Input Validation
All external input must be rigorously validated at the ingress boundary.

### Dependency Security
Dependencies must be checked by CI for vulnerabilities.
