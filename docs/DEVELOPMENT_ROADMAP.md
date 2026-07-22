# Development Roadmap

## Overview

This document outlines the phased development roadmap for Ads Detector, describing the sequence in which core features, modules, and capabilities are planned to be implemented, tested, and released. The roadmap is organized into phases aligned with the project's modular architecture and core workflow.

## Purpose

The purpose of this document is to:

- Provide a clear, shared understanding of development priorities and sequencing.
- Help contributors understand where a given feature fits within the overall delivery plan.
- Support release planning by grouping related functionality into coherent milestones.
- Serve as a living reference that is updated as priorities shift, with changes tracked in `PROJECT_DECISIONS.md` and `CHANGELOG.md`.

## Detailed Explanation

### Phase 1 — Foundation

- Establish core modular architecture: CSV Processor, Scanner Engine, Detection Engine, Database Layer, Export System, User Interface.
- Implement SQLite-based database schema per `DATABASE_DESIGN.md`.
- Implement CSV upload, validation, duplicate removal, and domain normalization (`FR-001` through `FR-003`).
- Establish baseline logging and error handling conventions.

### Phase 2 — Scanning and Detection Core

- Implement scan session creation and scan queue management (`FR-004`, `FR-005`).
- Implement the Website Scanner using Playwright-based browser automation (`FR-006`).
- Implement the initial rule-based Detection Engine covering advertising, tracking pixel, and analytics detection (`FR-007`).
- Implement Confidence Scoring as described in `CONFIDENCE_SCORING.md` (`FR-008`).
- Persist scan and detection results to the database (`FR-009`).

### Phase 3 — Dashboard and User Interaction

- Implement the Dashboard for viewing scan results (`FR-010`).
- Implement result management, including viewing detailed evidence per domain (`FR-011`).
- Implement the Filtering System across technology, confidence, tags, and star status (`FR-012`).
- Implement Star/Bookmark functionality (`FR-014`) and Notes/Tag management (`FR-015`).

### Phase 4 — Export and History

- Implement filtered Export functionality, ensuring only currently filtered results are exported (`FR-013`, `FR-020`).
- Implement Scan History tracking across repeated scans of the same domain (`FR-016`).
- Implement Application Settings for user-configurable behavior (`FR-017`).

### Phase 5 — Reliability and Hardening

- Expand error handling coverage across all modules per `ERROR_HANDLING.md`.
- Expand automated test coverage per `TESTING.md`, including edge cases identified in `KNOWN_LIMITATIONS.md`.
- Implement Notification System for scan completion and failure alerts (`FR-018`).
- Harden Security and Privacy controls (`FR-019`), including input validation and sandboxing of the Scanner Engine.

### Phase 6 — Deployment and Operability

- Finalize deployment procedures per `DEPLOYMENT.md`.
- Establish logging, monitoring, and performance baselines per `LOGGING.md` and `PERFORMANCE.md`.
- Prepare Docker-based deployment option per `DOCKER.md`.

## Functional Requirements

- Each roadmap phase must map to one or more functional requirement documents in `requirements/`.
- Features must not be marked complete until they satisfy the corresponding entries in `ACCEPTANCE_CRITERIA.md`.
- Roadmap phases may be reprioritized based on findings documented in `PROJECT_DECISIONS.md`, but reprioritization must be explicitly recorded rather than made silently.

## Technical Considerations

- The roadmap assumes SQLite as the initial database engine and Playwright as the scanning mechanism, per current technology decisions; any change to these decisions must trigger a roadmap review.
- Later phases (Dashboard, Filtering, Export) depend on stable output contracts from earlier phases (Detection Engine, Confidence Scoring); interface changes in early phases should be minimized once downstream phases begin implementation.
- Roadmap sequencing favors delivering an end-to-end vertical slice (upload → scan → detect → store → view) before expanding breadth (advanced filtering, notifications, history) to validate the core value proposition early.

## Workflow / Process

```
Phase Definition
      ↓
Functional Requirement Mapping
      ↓
Implementation
      ↓
Acceptance Criteria Verification
      ↓
Testing (Unit + Integration)
      ↓
Documentation Update
      ↓
Release Candidate
      ↓
Roadmap Status Update in CHANGELOG.md
```

## Error Handling

- If a phase cannot be completed due to a blocking technical constraint, the blocker must be documented in `KNOWN_LIMITATIONS.md` and the roadmap adjusted accordingly.
- Features delivered out of sequence (e.g., due to urgent client needs) must still be validated against their corresponding acceptance criteria before release.
- Any roadmap slippage that affects a dependent phase must be communicated by updating this document and referencing the change in `CHANGELOG.md`.

## Security Considerations

- Security and Privacy hardening (`FR-019`) must not be deferred indefinitely; baseline input validation and sandboxing must be present from Phase 2 onward, even though dedicated hardening occurs in Phase 5.
- Any roadmap acceleration that skips planned security work must be explicitly flagged and reviewed before release.
- Deployment and packaging work (Phase 6) must not proceed until the security hardening milestones from Phase 5 are complete.

## Future Improvements

- Introduce a formal milestone tracking board (e.g., GitHub Projects) that mirrors this roadmap for real-time status visibility.
- Add estimated effort and dependency graphs between functional requirements to support more precise sequencing.
- Expand the roadmap to include a post-launch phase covering user feedback incorporation and iterative refinement.
- Revisit phase boundaries once multi-user or API-consumer support is considered, as outlined in `KNOWN_LIMITATIONS.md`.

## Summary

The Development Roadmap defines a phased, dependency-aware sequence for building Ads Detector — from foundational CSV processing and modular architecture, through scanning and detection, dashboard interaction, export and history, reliability hardening, and finally deployment. Each phase is explicitly tied to functional requirements and acceptance criteria, ensuring that development progresses in a structured, verifiable manner aligned with the project's technology decisions and long-term vision.
