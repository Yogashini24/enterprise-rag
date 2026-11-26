# ADR-001: Local-first development

## Status
Accepted

## Context
We need a development environment that provides
control over infrastructure and reproducibility.

## Decision
Run the application, vector database,
metadata database and supporting services locally.

Use Docker Compose for infrastructure management.

## Consequences

Positive:
- Greater infrastructure control
- Lower infrastructure costs during development
- Reproducible local environments

Negative:
- Local resource requirements
- Infrastructure maintenance
- External connectivity required for LLM API calls