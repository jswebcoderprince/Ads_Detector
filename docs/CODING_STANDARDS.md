Coding Standards
Overview

This document defines the coding standards, style conventions, and engineering practices that all contributors to Ads Detector must follow. Consistent coding standards ensure that the codebase remains readable, maintainable, and predictable across all modules, regardless of which contributor authored a given piece of code. These standards apply to all languages and components used in the project, including the CSV Processor, Scanner Engine, Detection Engine, Database Layer, Export System, and User Interface.

Purpose

The purpose of this document is to:

Establish a single, unambiguous reference for code style across the entire codebase.
Reduce code review friction by removing subjective style debates.
Ensure long-term maintainability as the project scales and gains contributors.
Provide onboarding guidance for new developers joining the project.
Align implementation practices with the modular architecture described in SYSTEM_ARCHITECTURE.md.
Detailed Explanation
General Principles
Readability over cleverness. Code should be written to be understood by the next developer, not to demonstrate technical sophistication.
Explicit over implicit. Function names, variable names, and module boundaries should make intent obvious without requiring the reader to trace execution.
Single Responsibility. Each function, class, and module should do one thing. Modules such as the CSV Processor or Detection Engine must not absorb responsibilities belonging to other modules.
Consistency over personal preference. When in doubt, contributors follow the existing pattern in the surrounding code rather than introducing a new style.
Language and Formatting
Python is the primary backend language for CSV processing, scanning orchestration, detection logic, and database access.
Code must be formatted using an automated formatter (e.g., black) prior to commit. No manually formatted code should be merged if it diverges from the automated formatter's output.
Linting must be run using a standard linter (e.g., flake8 or ruff) as part of the pre-commit and CI pipeline.
Maximum line length is 100 characters unless breaking a line would harm readability (e.g., long URLs in comments).
Imports must be grouped in the standard order: standard library, third-party packages, local application modules — each group separated by a blank line.
Naming Conventions
Variables and functions: snake_case (e.g., normalize_domain, scan_queue).
Classes: PascalCase (e.g., DetectionEngine, ScanResult).
Constants: UPPER_SNAKE_CASE (e.g., MAX_CONCURRENT_SCANS, DEFAULT_TIMEOUT_SECONDS).
Private/internal members: prefixed with a single underscore (e.g., _internal_cache).
Names must describe intent, not implementation. domain_list is preferred over dl or temp1.
Module Structure
Each core module (CSV Processor, Scanner Engine, Detection Engine, Database Layer, Export System, User Interface) must live in its own clearly separated package/directory.
Cross-module communication must occur through well-defined interfaces (function signatures, data classes, or service objects) rather than direct access to another module's internal state.
Shared utilities (e.g., domain normalization helpers) belong in a common utils or shared module, not duplicated across modules.
Documentation and Comments
Every public function and class must include a docstring describing its purpose, parameters, return value, and any exceptions it may raise.
Comments should explain why, not what — the code itself should make the "what" self-evident through naming and structure.
Complex detection rules or scoring logic must include inline comments explaining the reasoning behind thresholds or evidence weighting.
Type Safety
Type hints are required for all function signatures, including parameters and return types.
Data structures passed between modules (e.g., scan results, detection evidence) should be defined using explicit data classes or typed dictionaries rather than untyped dictionaries.
Functional Requirements
All new code must pass automated linting and formatting checks before being merged.
All public interfaces must include type hints and docstrings.
Pull requests introducing new modules or significant refactors must include a brief design note referencing relevant sections of SYSTEM_ARCHITECTURE.md.
Technical Considerations
Coding standards must remain compatible with the modular architecture: CSV Processor, Scanner Engine, Detection Engine, Database Layer, Export System, and User Interface must each be independently testable.
Standards must account for the asynchronous nature of the Scanner Engine, which uses Playwright-based browser automation; asynchronous code must follow consistent async/await usage patterns rather than mixing synchronous and asynchronous styles within the same module.
Database access code must follow a consistent data access pattern (e.g., repository pattern) to avoid direct raw SQL scattered throughout business logic, in line with DATABASE_DESIGN.md.
Workflow / Process
Code Written
     ↓
Automated Formatter Applied
     ↓
Linter Executed
     ↓
Type Checker Executed
     ↓
Unit Tests Executed
     ↓
Pull Request Opened
     ↓
Peer Code Review (Standards Checklist)
     ↓
Merge to Main Branch
Contributors must run formatting, linting, and type-checking locally before opening a pull request.
Code review must explicitly verify adherence to naming conventions, module boundaries, and documentation requirements described in this file.
Error Handling
Coding standards violations detected in CI (formatting, linting, type errors) must block merge until resolved.
Exceptions must never be silently swallowed with a bare except: clause; all exception handling must specify the exception type and include appropriate logging, consistent with ERROR_HANDLING.md.
Functions that can fail in expected ways (e.g., network timeouts during scanning) must return explicit result/error structures rather than relying solely on exceptions for control flow.
Security Considerations
No secrets, API keys, or credentials may be hard-coded in source files; all sensitive configuration must be loaded from environment variables or a secrets manager, as described in CONFIGURATION.md.
User-supplied input (CSV contents, domain values, notes, tags) must be treated as untrusted and validated/sanitized before use in database queries or rendered output, to prevent injection and cross-site scripting vulnerabilities.
Code that interacts with external websites (Scanner Engine) must never execute or eval content returned by scanned sites outside of the sandboxed browser automation context.
Future Improvements
Introduce automated static analysis for security vulnerabilities (SAST) as part of the CI pipeline.
Expand type-checking enforcement using a strict static type checker (e.g., mypy --strict) once core modules stabilize.
Establish a formal style guide addendum for frontend/UI code if the User Interface layer expands to a dedicated frontend framework.
Introduce architecture decision record (ADR) requirements for any change that affects module boundaries.
Summary

This document establishes the coding standards that govern all contributions to Ads Detector, covering formatting, naming, module structure, documentation, and type safety. Adherence to these standards ensures the codebase remains consistent, readable, and maintainable as the project grows, and ensures that engineering practices remain aligned with the modular architecture and technology decisions that define the platform.
