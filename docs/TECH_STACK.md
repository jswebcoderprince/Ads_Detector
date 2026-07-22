# Tech Stack

## Overview

This document catalogs the technology stack used to build and operate Ads Detector, including the programming language, core libraries, database, browser automation framework, and supporting tooling. It serves as a single reference point for understanding what technologies power each layer of the modular architecture.

## Purpose

The purpose of this document is to:

- Provide a clear, centralized inventory of all technologies used across the platform.
- Explain the reasoning behind key technology choices, cross-referencing `PROJECT_DECISIONS.md` where applicable.
- Support onboarding by giving new contributors a quick orientation to the tools they will work with.
- Serve as a reference point when evaluating future technology changes or additions.

## Detailed Explanation

### Core Language

- **Python** — the primary language for all backend logic, including the CSV Processor, Scanner Engine orchestration, Detection Engine, Database Layer, and Export System. Chosen for its strong ecosystem of data processing, automation, and testing libraries.

### Browser Automation

- **Playwright** — used by the Scanner Engine to perform full browser-based rendering and network interception of scanned websites, as detailed in `PLAYWRIGHT_ENGINE.md`. Chosen over lightweight HTTP-only scraping approaches because many advertising, tracking, and analytics technologies only become observable after JavaScript execution and full page rendering.

### Database

- **SQLite** — the initial database engine for persisting scan results, detection evidence, confidence scores, tags, notes, and star status, as detailed in `DATABASE_DESIGN.md`. Chosen for simple deployment, easy backup, and strong support for local, single-instance application usage.

### CSV Processing

- **pandas** (or equivalent tabular data library) — used for parsing, validating, and transforming uploaded CSV files, supporting column detection, normalization, and duplicate removal as described in `CSV_PROCESSING_ENGINE.md`.

### Detection Rules

- **Rule-based, configuration-driven matching logic** — the Detection Engine relies on structured pattern-matching rules (URL patterns, cookie signatures, header signatures) rather than machine learning models, keeping detection explainable and auditable, as detailed in `DETECTION_ENGINE.md`.

### Application Packaging and Deployment

- **Docker** — used to containerize the application and its dependencies, including Playwright's browser binaries, for consistent deployment across environments, as detailed in `DOCKER.md` and `DEPLOYMENT.md`.

### Testing

- **pytest** (or equivalent Python testing framework) — used for unit and integration testing across all modules, as detailed in `TESTING.md`.

### Code Quality Tooling

- **Formatter** (e.g., `black`) and **linter** (e.g., `flake8` or `ruff`) — enforced as part of the development workflow described in `CODING_STANDARDS.md`.

### User Interface

- A web-based User Interface layer providing the Dashboard, Filtering System, and Star/Notes/Tags management, consuming data exposed by the Database Layer through the application's internal API, as described in `API_SPECIFICATION.md`.

## Functional Requirements

- All technology choices documented here must remain consistent with the decisions recorded in `PROJECT_DECISIONS.md`; any deviation must be reflected as an update in both documents.
- New dependencies introduced into the codebase must be added to this document as part of the same pull request.
- Version pinning must be maintained for all core dependencies (Python packages, Playwright, browser binaries) to ensure reproducible builds.

## Technical Considerations

- The tech stack is deliberately kept lean and Python-centric to minimize operational complexity for a platform initially targeting single-user or small-team, locally-deployed usage.
- SQLite's suitability is directly tied to the platform's current concurrency and deployment scale; a future migration to a client-server database (e.g., PostgreSQL) would be a significant architectural change requiring updates across `DATABASE_DESIGN.md`, `DEPLOYMENT.md`, and this document.
- Playwright's browser binary requirements introduce a meaningful dependency footprint that must be accounted for in containerization (`DOCKER.md`) and deployment planning (`DEPLOYMENT.md`).

## Workflow / Process

```
Technology Need Identified
              ↓
Evaluated Against Existing Stack and Project Constraints
              ↓
Decision Recorded in PROJECT_DECISIONS.md
              ↓
Technology Adopted and Documented in TECH_STACK.md
              ↓
Dependency Version Pinned in Project Manifest
              ↓
Adoption Reflected in Onboarding and CI Configuration
```

## Error Handling

- Dependency version mismatches (e.g., Playwright library version vs. installed browser binary version) must be caught at build or startup time with a clear error, rather than surfacing as obscure runtime failures during scanning.
- Missing or incompatible system-level dependencies (e.g., libraries required by headless browser execution) must be validated during the Docker build process, as described in `DOCKER.md`.

## Security Considerations

- All third-party dependencies must be sourced from trusted, official package registries and periodically reviewed for known vulnerabilities.
- Version pinning reduces the risk of an unreviewed dependency update introducing a security regression; updates must go through the standard code review process.
- The technology stack must avoid unnecessary dependencies that expand the application's attack surface, particularly around the Scanner Engine's browser automation layer.

## Future Improvements

- Evaluate introducing a dedicated frontend framework for the User Interface layer if the Dashboard's interactivity requirements grow beyond what the current implementation supports.
- Assess migration paths from SQLite to a client-server database as usage scales beyond single-instance deployment.
- Consider adopting a task queue system (e.g., for asynchronous scan orchestration) if scan volume grows to require distributed processing.
- Periodically re-evaluate browser automation alternatives to Playwright as the ecosystem evolves, ensuring the platform continues to use the most capable and well-maintained tooling available.

## Summary

The Ads Detector technology stack centers on Python for backend logic, Playwright for browser automation and network capture, and SQLite for lightweight, easily deployable data persistence. This document serves as the authoritative inventory of these technologies, their rationale, and their interdependencies, supporting consistent onboarding, dependency management, and future architectural planning.
