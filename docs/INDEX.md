# Documentation Index

## Overview

This document serves as the central index for all technical and product documentation contained within the `docs/` directory of Ads Detector. It provides a quick-reference map of every document, grouped by category, so contributors and stakeholders can quickly locate the information they need.

## Purpose

The purpose of this document is to:

- Provide a single entry point for navigating the full documentation set.
- Group related documents by category (Product, Requirements, Architecture, Engineering, Operations) for faster discovery.
- Reflect the high-level documentation flow that a new contributor should follow when onboarding.
- Stay in sync with the actual contents of `docs/` as new files are added.

## Detailed Explanation

### Recommended Reading Order

```
Product Vision
      ↓
Project Scope
      ↓
Business Requirements
      ↓
Functional Overview
      ↓
User Stories
      ↓
Non-Functional Requirements
      ↓
System Architecture
      ↓
Detailed Engine Documentation
      ↓
Testing
      ↓
Deployment
```

### Product Documentation

- `PRODUCT_VISION.md` — the long-term vision and purpose of Ads Detector.
- `PROJECT_SCOPE.md` — what is and is not included in the current scope of the project.
- `PROJECT_DECISIONS.md` — a record of key technical and product decisions and their rationale.
- `BUSINESS_REQUIREMENTS.md` — business-level requirements driving the product.
- `FUNCTIONAL_OVERVIEW.md` — a functional summary of what the system does.
- `USER_STORIES.md` — user stories describing platform usage from the end user's perspective.
- `NON_FUNCTIONAL_REQUIREMENTS.md` — quality attributes such as performance, reliability, and usability expectations.
- `KNOWN_LIMITATIONS.md` — current known limitations and constraints of the platform.
- `ACCEPTANCE_CRITERIA.md` — testable, measurable conditions that define feature completeness.
- `DEVELOPMENT_ROADMAP.md` — the phased plan for building out the platform's features.
- `GLOSSARY.md` — a shared reference of terms and acronyms used across the documentation.

### Architecture and Engineering Documentation

- `SYSTEM_ARCHITECTURE.md` — the overall modular architecture of the platform.
- `API_SPECIFICATION.md` — the internal API contract used by the User Interface and other consumers.
- `DATABASE_DESIGN.md` — the database schema and data model.
- `CSV_PROCESSING_ENGINE.md` — CSV upload, validation, and normalization logic.
- `SCANNER_ENGINE.md` — the website scanning module and its orchestration.
- `PLAYWRIGHT_ENGINE.md` — the Playwright-based browser automation implementation details.
- `DETECTION_ENGINE.md` — the rule-based technology detection logic.
- `CONFIDENCE_SCORING.md` — the confidence scoring methodology applied to detections.
- `EXPORT_ENGINE.md` — the filtered export generation module.
- `CODING_STANDARDS.md` — code style, naming, and engineering conventions.
- `CONFIGURATION.md` — application configuration sources and parameters.
- `TECH_STACK.md` — the full technology stack used across the platform.

### Quality and Operations Documentation

- `TESTING.md` — testing strategy and coverage expectations.
- `ERROR_HANDLING.md` — error handling conventions across all modules.
- `LOGGING.md` — logging strategy and structured log format.
- `PERFORMANCE.md` — performance expectations and optimization strategies.
- `SECURITY.md` — consolidated security practices and threat model.
- `DEPLOYMENT.md` — deployment procedures and environment setup.
- `DOCKER.md` — containerization strategy and Docker configuration.
- `UI_UX_SPECIFICATION.md` — user interface and user experience specification.
- `AI_IMPLEMENTATION_RULES.md` — rules and constraints governing AI-assisted implementation of the platform.

## Functional Requirements

- Every new document added to `docs/` must be added to this index under the appropriate category in the same pull request.
- This index must never reference a document that does not exist in `docs/`, and every document in `docs/` must be referenced somewhere in this index.

## Technical Considerations

- This index is a navigation aid only; it does not duplicate content from the documents it references. Contributors should treat each linked document as the single source of truth for its subject matter.
- Categories in this index are expected to evolve as the platform grows; new categories may be introduced if a cluster of related documents no longer fits cleanly into Product, Architecture/Engineering, or Quality/Operations.

## Workflow / Process

```
New Documentation File Created
              ↓
File Placed in docs/ Following Existing Naming Conventions
              ↓
Entry Added to This Index Under the Correct Category
              ↓
Pull Request Reviewed for Both Content and Index Accuracy
              ↓
Merged to Main Branch
```

## Error Handling

- If a broken or missing reference is discovered in this index (e.g., a renamed or deleted file), it must be corrected as part of the pull request that introduced the discrepancy, not deferred.

## Security Considerations

- Not directly applicable; however, this index must not reference internal-only or sensitive documents (if any are introduced in the future) in a way that would be inappropriate for the intended audience of the `docs/` directory.

## Future Improvements

- Generate this index automatically from front-matter metadata in each document once the documentation set grows large enough to warrant tooling support.
- Add short one-line summaries next to each linked document for faster scanning.
- Introduce a versioned changelog specifically for documentation updates, separate from the main `CHANGELOG.md`.

## Summary

This index provides a categorized, navigable map of all documentation within `docs/`, guiding contributors from product vision through architecture, engineering detail, and operational practices. Keeping this index accurate and up to date ensures that the documentation set remains discoverable and useful as Ads Detector continues to grow.
