# ADR 004: PostgreSQL as Durable Source of Truth

## Status
Accepted

## Context
The platform needs to store configuration, state, audit logs, and identity information (RBAC). This data must be highly durable, structured, and support complex relational queries (e.g., "Which services is this user allowed to deploy based on their team membership?").

## Decision
PostgreSQL will be the primary durable source of truth for the IDP.

## Consequences
- Requires maintaining schema migrations.
- Provides strong consistency guarantees for audit and state records.
- Other data stores (like Redis) will be used strictly for ephemeral or non-critical state.

## Alternatives considered
- **NoSQL (e.g., MongoDB):** Rejected because the data model is highly relational and requires strong ACID guarantees.
