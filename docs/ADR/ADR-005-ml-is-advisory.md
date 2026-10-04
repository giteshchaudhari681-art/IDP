# ADR 005: ML is Advisory

## Status
Accepted

## Context
We want to predict deployment failures based on historical data (e.g., GitHub webhooks, past build events). However, ML models can be inaccurate, suffer from concept drift, or go offline.

## Decision
The ML prediction pipeline will be purely advisory and non-load-bearing. It will provide failure probability scores for deployments but will NEVER automatically block a deployment based on a high risk score, nor will its unavailability prevent a deployment from proceeding.

## Consequences
- The deployment path remains robust even if the ML service crashes.
- We avoid "black box" blocking of developer workflows.
- Predictions are surfaced to the user for them to make informed decisions.

## Alternatives considered
- **ML as a blocking gate:** Rejected due to reliability concerns and the risk of false positives preventing critical hotfixes.
