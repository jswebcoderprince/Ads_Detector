# Acceptance Criteria

## Overview

This document defines the formal acceptance criteria for the Ads Detector platform. Acceptance criteria describe the measurable, testable conditions that must be satisfied for a feature, module, or release to be considered complete and production-ready. These criteria serve as the contract between product requirements and engineering implementation, and they are used by developers, QA engineers, and reviewers to validate that delivered functionality matches the intended behavior of the system.

Acceptance criteria in this document are organized by functional area, mirroring the core workflow of Ads Detector: CSV Upload → CSV Validation → Domain Processing → Scan Queue → Website Scanner → Detection Engine → Confidence Scoring → Database Storage → Dashboard → Filtering → Star/Notes/Tags → Export Results.

## Purpose

The purpose of this document is to:

- Establish an unambiguous definition of "done" for every major feature of Ads Detector.
- Provide a reference checklist for QA and code review sign-off.
- Reduce subjective interpretation of requirements during development.
- Ensure consistency between `PROJECT_SCOPE.md`, `PRODUCT_VISION.md`, and actual delivered behavior.
- Serve as the basis for automated and manual test case design referenced in `TESTING.md`.
- Prevent scope drift by anchoring feature completeness to explicit, verifiable conditions.

Acceptance criteria are not implementation instructions. They describe **outcomes**, not **methods**. Engineering teams retain flexibility in how a criterion is satisfied, as long as the observable behavior matches the specification.

## Detailed Explanation

Each functional area below is broken into individual acceptance criteria. Every criterion follows a Given/When/Then structure where applicable, to keep conditions testable and traceable.

### 1. CSV Upload

**AC-1.1 — Valid CSV Acceptance**
Given a user uploads a `.csv` file containing a column of domain names,
When the file is submitted through the upload interface,
Then the system must accept the file and proceed to the validation stage without error.

**AC-1.2 — File Type Restriction**
Given a user attempts to upload a non-CSV file (e.g., `.xlsx`, `.txt`, `.json`),
When the file is submitted,
Then the system must reject the file and display a clear, descriptive error message indicating the accepted format.

**AC-1.3 — File Size Limit**
Given a CSV file exceeds the configured maximum file size,
When the upload is attempted,
Then the system must reject the upload and inform the user of the maximum allowed size.

**AC-1.4 — Empty File Handling**
Given a CSV file contains no rows or only a header row,
When the file is uploaded,
Then the system must reject the file with a message indicating no valid domains were found.

### 2. CSV Validation

**AC-2.1 — Column Detection**
Given a CSV file with a domain-containing column (regardless of header naming variations such as `domain`, `url`, `website`),
When validation runs,
Then the system must correctly identify and map the domain column automatically or prompt the user for column selection if ambiguous.

**AC-2.2 — Malformed Row Rejection**
Given a CSV file contains rows with malformed, empty, or non-domain values,
When validation runs,
Then those specific rows must be flagged and excluded from processing, and the user must receive a summary report of excluded rows.

**AC-2.3 — Encoding Handling**
Given a CSV file is encoded in UTF-8, UTF-8 with BOM, or common regional encodings,
When the file is parsed,
Then the system must correctly decode the content without corrupting domain values.

**AC-2.4 — Validation Summary Reporting**
Given a CSV file has completed validation,
When the process finishes,
Then the system must present a summary containing: total rows read, valid rows, invalid rows, and duplicate rows detected.

### 3. Domain Processing

**AC-3.1 — Domain Normalization**
Given raw domain values may include protocols, trailing slashes, subdomain variants, or mixed casing (e.g., `HTTPS://Example.com/`),
When domain processing runs,
Then all domains must be normalized to a canonical lowercase, protocol-stripped format (e.g., `example.com`).

**AC-3.2 — Duplicate Removal**
Given a CSV file contains duplicate domains (exact or normalized-equivalent),
When domain processing runs,
Then duplicates must be removed, and only a single canonical entry per domain must proceed to the scan queue.

**AC-3.3 — Invalid Domain Filtering**
Given a value cannot be parsed into a valid domain structure (e.g., missing TLD, invalid characters),
When domain processing runs,
Then the value must be excluded and logged in the invalid domains report.

**AC-3.4 — Subdomain Handling Consistency**
Given the input contains both a root domain and its subdomain (e.g., `example.com` and `shop.example.com`),
When domain processing runs,
Then both must be treated as distinct scan targets unless configured otherwise.

### 4. Scan Queue

**AC-4.1 — Queue Population**
Given domain processing has completed successfully,
When the scan queue is populated,
Then every valid, unique, normalized domain must be added to the queue exactly once.

**AC-4.2 — Queue Ordering**
Given multiple domains are queued for scanning,
When the scanner begins execution,
Then domains must be processed in a deterministic, first-in-first-out order unless a priority mechanism is explicitly configured.

**AC-4.3 — Concurrent Scan Limits**
Given system configuration defines a maximum concurrency limit,
When the scan queue is actively processing,
Then the number of simultaneous active scans must never exceed the configured limit.

**AC-4.4 — Queue Persistence**
Given the application is interrupted or restarted while scans are queued,
When the application resumes,
Then previously queued but unprocessed domains must remain in the queue and not be lost.

### 5. Website Scanner

**AC-5.1 — Successful Page Load**
Given a domain is reachable and returns a valid HTTP response,
When the scanner visits the site using Playwright browser automation,
Then the scanner must capture the rendered DOM, network requests, and response headers required for detection.

**AC-5.2 — Timeout Handling**
Given a domain does not respond within the configured timeout window,
When the scan is attempted,
Then the scanner must mark the domain as "unreachable" or "timeout" and proceed to the next queued domain without halting the overall scan process.

**AC-5.3 — Redirect Handling**
Given a domain redirects to a different URL (HTTP redirect or JavaScript redirect),
When the scanner processes the domain,
Then the scanner must follow the redirect chain up to a configured maximum depth and record the final resolved URL.

**AC-5.4 — Blocked/Restricted Site Handling**
Given a domain returns a CAPTCHA challenge, bot-detection block, or access-denied response,
When scanning is attempted,
Then the scanner must record this outcome distinctly (e.g., "blocked") rather than reporting a false negative for technology detection.

**AC-5.5 — Resource Capture Completeness**
Given a website loads external scripts, tracking pixels, and third-party network requests,
When the scan executes,
Then the scanner must capture all network requests, response headers, cookies set, and relevant DOM elements needed for the Detection Engine.

### 6. Detection Engine

**AC-6.1 — Advertising Technology Detection**
Given a scanned website loads known advertising network scripts or ad server requests,
When the Detection Engine analyzes captured scan data,
Then it must correctly identify and label the specific advertising technology per the detection rule set defined in `DETECTION_ENGINE.md`.

**AC-6.2 — Tracking Pixel Detection**
Given a scanned website contains tracking pixel requests (e.g., Facebook Pixel, conversion tracking beacons),
When detection runs,
Then each identified tracking pixel must be recorded with its associated evidence (request URL, matched pattern).

**AC-6.3 — Analytics Detection**
Given a scanned website includes analytics scripts (e.g., Google Analytics, other analytics providers),
When detection runs,
Then the analytics technology must be identified and attributed with supporting evidence.

**AC-6.4 — Evidence Attachment**
Given any technology is detected on a scanned website,
When the detection result is generated,
Then the result must include the specific evidence used to justify the detection (matched request, script signature, cookie name, or header value).

**AC-6.5 — No False Detection Without Evidence**
Given no matching detection rule is triggered for a given technology category,
When the Detection Engine finalizes results,
Then that technology category must not appear in the results for that domain.

### 7. Confidence Scoring

**AC-7.1 — Score Assignment**
Given one or more detection rules match for a given technology,
When confidence scoring is calculated,
Then a numeric or categorical confidence score must be assigned based on the strength and quantity of matched evidence.

**AC-7.2 — Score Consistency**
Given identical scan evidence is processed on two separate occasions,
When confidence scoring is applied,
Then the resulting score must be identical (deterministic scoring, no randomness).

**AC-7.3 — Score Range Validation**
Given the confidence scoring system defines a fixed scoring scale (e.g., 0–100 or Low/Medium/High),
When any score is generated,
Then it must fall strictly within the defined scale boundaries.

### 8. Database Storage

**AC-8.1 — Result Persistence**
Given a domain scan and detection cycle completes,
When results are finalized,
Then all scan metadata, detection results, evidence, and confidence scores must be persisted to the database without data loss.

**AC-8.2 — Referential Integrity**
Given a domain has multiple historical scans,
When new scan results are stored,
Then existing historical scan records must remain intact and correctly associated with their respective domain.

**AC-8.3 — Transactional Safety**
Given a failure occurs mid-write during database storage,
When the failure is detected,
Then the system must roll back incomplete transactions to avoid partial or corrupted records.

### 9. Dashboard

**AC-9.1 — Result Visibility**
Given scans have completed and results are stored,
When a user opens the dashboard,
Then all scanned domains must be visible with their key metadata: detected technologies, confidence scores, scan date, and scan status.

**AC-9.2 — Real-Time/Near-Real-Time Status Updates**
Given scans are actively in progress,
When a user views the dashboard,
Then in-progress, completed, and failed scan statuses must be accurately reflected.

**AC-9.3 — Performance Under Load**
Given the database contains a large volume of scanned domains (e.g., 10,000+),
When the dashboard is loaded,
Then the interface must remain responsive through pagination, lazy loading, or equivalent performance optimization.

### 10. Filtering System

**AC-10.1 — Technology-Based Filtering**
Given a user selects one or more detected technology filters (e.g., "Google Analytics", "Facebook Pixel"),
When the filter is applied,
Then only domains matching all selected filter criteria must be displayed.

**AC-10.2 — Confidence Score Filtering**
Given a user sets a minimum confidence threshold,
When the filter is applied,
Then only results meeting or exceeding that threshold must be displayed.

**AC-10.3 — Combined Filter Logic**
Given multiple filter types are applied simultaneously (technology, confidence, tags, star status),
When filters are combined,
Then results must satisfy all active filter conditions (logical AND) unless the interface explicitly supports OR-based filtering.

**AC-10.4 — Filter Reset**
Given filters are currently applied,
When the user resets filters,
Then the full unfiltered result set must be restored.

### 11. Star / Notes / Tags

**AC-11.1 — Starring a Domain**
Given a user marks a domain as "starred,"
When the action is saved,
Then the star status must persist across sessions and be reflected in filtering and export options.

**AC-11.2 — Adding Notes**
Given a user adds a free-text note to a domain,
When the note is saved,
Then it must be retrievable, editable, and persist independently of scan re-runs.

**AC-11.3 — Adding Tags**
Given a user assigns one or more tags to a domain,
When tags are saved,
Then they must be available for use in the filtering system and must support multiple tags per domain.

**AC-11.4 — Data Independence from Scans**
Given a domain is re-scanned,
When new scan results are generated,
Then existing stars, notes, and tags must not be overwritten or deleted.

### 12. Export Results

**AC-12.1 — Filtered Export Only**
Given a user has applied filters to the dashboard results,
When an export action is triggered,
Then only the currently filtered result set must be included in the export file, not the entire database.

**AC-12.2 — Export Format Integrity**
Given an export is generated,
When the output file is opened,
Then it must be a valid, well-formed CSV (or configured format) containing all relevant columns: domain, detected technologies, confidence scores, tags, notes, star status, and scan date.

**AC-12.3 — Export Completion Confirmation**
Given an export process completes successfully,
When the user is notified,
Then a clear confirmation and download link/path must be provided.

## Functional Requirements

- Each acceptance criterion listed above must map to at least one automated or manual test case in the test suite referenced in `TESTING.md`.
- No feature may be marked "release-ready" unless all associated acceptance criteria pass.
- Acceptance criteria must be reviewed and updated whenever `PROJECT_SCOPE.md` or `PRODUCT_VISION.md` changes.
- All criteria must remain technology-agnostic where possible, describing behavior rather than implementation.

## Technical Considerations

- Acceptance criteria assume the underlying architecture described in `SYSTEM_ARCHITECTURE.md`, including the modular separation of CSV Processor, Scanner Engine, Detection Engine, Database Layer, Export System, and User Interface.
- Criteria involving the Scanner Engine assume Playwright-based browser automation as the execution mechanism, per current technology decisions.
- Criteria involving persistence assume SQLite as the initial database engine; criteria are written to remain valid if the database layer is later migrated to another RDBMS.
- Confidence scoring criteria must remain compatible with the rule-based, evidence-driven detection model defined in `DETECTION_ENGINE.md`.
- Performance-related criteria (e.g., AC-9.3) should be validated against realistic production data volumes, not just development-scale datasets.

## Workflow / Process

The acceptance criteria validation process follows this lifecycle:

```
Feature Implementation
        ↓
Developer Self-Verification (against relevant AC section)
        ↓
Automated Test Execution (unit + integration)
        ↓
Manual QA Verification (exploratory + AC checklist)
        ↓
Code Review Sign-off
        ↓
Acceptance Criteria Checklist Completion
        ↓
Merge to Main Branch
        ↓
Release Candidate Tagging
```

Each pull request that implements or modifies a feature covered in this document must reference the specific acceptance criteria IDs (e.g., AC-6.2, AC-10.3) it satisfies in the PR description.

## Error Handling

- If an acceptance criterion cannot be fully satisfied due to a technical constraint, the deviation must be documented in `KNOWN_LIMITATIONS.md` with justification.
- Any regression that causes a previously passing acceptance criterion to fail must be treated as a release-blocking defect.
- Ambiguous or conflicting acceptance criteria must be flagged during code review and resolved through discussion documented in `PROJECT_DECISIONS.md` before implementation proceeds.
- Test failures tied to specific AC IDs must be logged with the AC identifier for traceability.

## Security Considerations

- Acceptance criteria involving file uploads (AC-1.1 through AC-1.4) must be validated alongside security testing for malicious file content, oversized payloads, and injection attempts through CSV fields.
- Acceptance criteria involving the Scanner Engine must ensure that scanning untrusted third-party websites does not expose the host system to script execution risks outside the sandboxed browser automation context.
- Export functionality (AC-12.1–AC-12.3) must be validated to ensure exported files do not leak internal system data (e.g., raw database identifiers, internal error traces) beyond what is intended for the user.
- Notes and tags fields (AC-11.2, AC-11.3) must be validated against stored cross-site scripting (XSS) risks if rendered in a web-based dashboard.

## Future Improvements

- Introduce automated acceptance-test-to-requirement traceability tooling that cross-references AC IDs directly with test suite results.
- Expand acceptance criteria to cover multi-user and role-based access scenarios as the platform evolves beyond single-user/local deployment.
- Add acceptance criteria for API-level consumers once `API_SPECIFICATION.md` capabilities expand to support third-party integrations.
- Define acceptance criteria for internationalization/localization if the platform expands beyond its current target markets.
- Establish performance-specific acceptance criteria with quantified benchmarks (e.g., maximum dashboard load time at defined record counts) as the system matures.

## Summary

This document establishes the definitive, testable acceptance criteria for all core functional areas of Ads Detector, from CSV upload through export of filtered results. Each criterion is written to be unambiguous, verifiable, and traceable to both product requirements and test coverage. Acceptance criteria act as the final gatekeeper for feature completeness and release readiness, ensuring that Ads Detector consistently delivers reliable, evidence-based advertising and tracking technology detection in accordance with its stated product vision and architectural decisions.
