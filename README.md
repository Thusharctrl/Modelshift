# ModelShift

ModelShift is a proposed local-first, CLI-first developer tool for discovering AI model dependencies, checking their lifecycle status against official evidence, and evaluating a proposed replacement against saved baselines.

## Problem

Model identifiers are often embedded in source code and configuration. Provider lifecycle notices can be missed, and a replacement that appears to work can still break downstream expectations. ModelShift is intended to make those risks visible and testable without claiming that a migration is safe for production.

## Proposed core capabilities

The current draft proposes a workflow of repository scan, dependency inventory, lifecycle verification, baseline comparison, and local HTML/JSON reporting. Its initial supported scope is Python and selected configuration formats; lifecycle information must retain official source evidence and verification timestamps; comparison uses deterministic validators and marks absent baselines as inconclusive.

These are proposed MVP directions, not approved implementation commitments.

## Development status

The project is in documentation and scope-validation stage. No application code, dependencies, virtual environment, architecture decision, or integration has been created. Product and technical decisions must be finalized before a technical requirements document (TRD) or implementation begins.

## Documentation

- [Project status](docs/PROJECT_STATUS.md)
- [PRD audit](docs/PRD_AUDIT.md)
- [Open decisions](docs/OPEN_DECISIONS.md)
- [Draft PRD (v1.0)](docs/reference/ModelShift_PRD_v1.0.pdf)
