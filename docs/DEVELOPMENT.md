# Development Standards

This document establishes the expected engineering workflow for the IDP. *Note: Commands that depend on future infrastructure are not yet available.*

## Repository setup
Clone the repository and install dependencies (future CI tooling will enforce environments).

## Branch creation
Always branch off the default branch using feature branches (e.g., `feat/pr-XX-name`).

## Development
Follow the strict 100-PR progression. Never leak future scope into the current PR.

## Testing
Write unit and integration tests as applicable to the component being built. 

## Formatting
All code must be formatted using the standard formatter (to be established in a future PR).

## Linting
All code must pass the standard linter checks.

## Type checking
All TypeScript code must pass strict type checking.

## Building
All components must compile without errors.

## Commit conventions
Use conventional commits (e.g., `feat:`, `fix:`, `docs:`, `chore:`).

## CI expectations
All PRs must pass the CI quality gates. A failure must be investigated, not hidden.

## PR expectations
- One PR = One defined milestone from the roadmap.
- PRs must be manually reviewed.
- PRs must pass a future-scope leakage audit.

## Debugging expectations
Use structured logging and traces when debugging services in the future.

## Environment variable handling
Environment variables should be strictly validated at startup.

## Secret handling
Do NOT commit secrets. Use secure secret injection at runtime.
