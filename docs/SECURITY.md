# Security

## Overview

This document consolidates the security posture and practices governing Ads Detector, covering input validation, sandboxing of the Scanner Engine, data protection, and secure deployment practices. Security is a cross-cutting concern that touches every module of the system — CSV Processor, Scanner Engine, Detection Engine, Database Layer, Export System, and User Interface.

## Purpose

The purpose of this document is to:

- Establish a centralized reference for security practices across the entire application.
- Define how the system protects itself from risks introduced by processing untrusted CSV input and scanning untrusted third-party websites.
- Ensure data handled by the platform (domains, notes, tags, scan results) is stored and exposed safely.
- Support compliance with the security-related functional requirement `FR-019_SECURITY_AND_PRIVACY.md`.

## Detailed Explanation

### Threat Model

Ads Detector faces two primary categories of untrusted input:

1. **User-supplied data** — CSV uploads, notes, tags, and filter inputs provided directly by the application's users.
2. **Third-party website content** — the actual content, scripts, and network behavior of websites being scanned, which is inherently untrusted and potentially malicious.

### Input Validation

- All CSV input must be validated and sanitized before processing, per `CSV_PROCESSING_ENGINE.md`, including rejection of malformed rows, oversized files, and unsupported encodings.
- Notes and tags fields must be treated as untrusted user input; they must be sanitized before storage and before rendering in any UI context to prevent stored cross-site scripting (XSS).
- Filter inputs used to construct database queries must use parameterized queries exclusively; raw string concatenation into SQL statements is prohibited.

### Scanner Sandboxing

- The Scanner Engine, via the Playwright Engine, visits arbitrary third-party websites. Each scan runs in an isolated, sandboxed browser context to prevent scanned sites from affecting the host system, other scans, or persisted application state.
- Scanned websites must never be permitted to trigger file downloads, native OS dialogs, or interactions that could affect the host environment.
- Outbound network requests made during scanning are expected and intentional; however, the scanning environment itself must not have access to internal application secrets, the database file, or other non-scanning-related resources.

### Data Protection

- The SQLite database file must be protected with appropriate file system permissions, accessible only to the application process and authorized administrators.
- No personally identifiable information beyond what is necessary (domain names, user-entered notes/tags) is collected or stored by the platform.
- Export files must be sanitized to prevent CSV injection (formula injection) and must not include internal identifiers or diagnostic data not intended for end users.

### Secure Configuration

- Secrets and credentials must never be hard-coded or committed to version control, per `CONFIGURATION.md`.
- Environment-specific configuration must clearly separate development, testing, and production settings to prevent accidental use of production credentials in non-production contexts.

## Functional Requirements

- All user-supplied input (CSV content, notes, tags, filters) must be validated and sanitized before being processed, stored, or rendered.
- The Scanner Engine must operate scanned websites within an isolated browser sandbox at all times.
- Export functionality must sanitize output to prevent injection attacks when opened in spreadsheet applications.
- Access to the underlying database file and export output directory must be restricted at the file system level.

## Technical Considerations

- Security controls must be layered across the modular architecture: input validation at the CSV Processor and User Interface boundary, sandboxing at the Scanner Engine, parameterized access at the Database Layer, and output sanitization at the Export System.
- Because the Scanner Engine intentionally connects to arbitrary external domains, standard network security assumptions (e.g., "only trusted destinations") do not apply; sandboxing and isolation are the primary controls rather than network allow-listing.
- Dependency management must include periodic review of third-party packages (including Playwright) for known vulnerabilities.

## Workflow / Process

```
Untrusted Input Received (CSV, Notes, Tags, Filters)
              ↓
Input Validated and Sanitized at Entry Point
              ↓
Scanner Engine Visits Untrusted Third-Party Site (Sandboxed)
              ↓
Captured Data Passed Through Detection Engine (No Code Execution)
              ↓
Results Stored via Parameterized Database Access
              ↓
Output Rendered/Exported with Sanitization Applied
```

## Error Handling

- Security-relevant failures (e.g., a blocked scan due to sandbox violation, a rejected malformed CSV row) must be logged with sufficient context for review, per `LOGGING.md`, without exposing sensitive details to end users.
- Validation failures must return clear, generic error messages to users, avoiding the disclosure of internal implementation details that could aid an attacker.

## Security Considerations

- This document intentionally overlaps with security-relevant sections of other documents (`CODING_STANDARDS.md`, `CONFIGURATION.md`, `DOCKER.md`, `PLAYWRIGHT_ENGINE.md`, `EXPORT_ENGINE.md`); this file serves as the consolidated entry point, while implementation-specific detail remains in each respective document.
- Regular security review of the detection ruleset is recommended, since rules are configuration-driven and could be a target for tampering if configuration access is not properly restricted.
- All security-relevant configuration changes must be reviewed and documented in `PROJECT_DECISIONS.md`.

## Future Improvements

- Introduce automated dependency vulnerability scanning as part of the CI pipeline.
- Add rate limiting on CSV upload and export endpoints to mitigate abuse or resource-exhaustion attempts.
- Evaluate formal penetration testing once the platform moves beyond single-user/local deployment toward broader multi-user use.
- Expand sandboxing controls if the Scanner Engine is extended to support more complex website interactions (e.g., simulated clicks or form submissions).

## Summary

Security in Ads Detector is addressed as a cross-cutting concern spanning input validation, browser sandboxing, data protection, and secure configuration. Because the platform's core function requires processing untrusted user input and scanning untrusted third-party websites, isolation and validation are treated as first-class architectural requirements rather than afterthoughts, ensuring the platform can be operated safely even as scan volume and user base grow.
