# Non Functional Requirements

## Overview

This document defines the quality attributes and technical standards that Ads Detector must follow.

While functional requirements describe application features, non-functional requirements define how the system should perform, behave, and remain maintainable.

---

# 1. Performance Requirements

## NFR-001: Fast Application Response

The application should provide fast responses during normal user interactions.

Examples:

- CSV upload should complete quickly.
- Dashboard loading should be responsive.
- Filtering should happen without noticeable delay.

---

## NFR-002: Large CSV Support

The system should support processing large CSV files.

Target:

```
Minimum:
1,000 websites

Future Goal:
10,000+ websites
```

The application should avoid crashing during large imports.

---

## NFR-003: Efficient Scanning

The scanner should process websites efficiently.

The system should support:

- Controlled concurrency
- Queue management
- Resource monitoring

The user should be able to configure scanning speed based on their machine capability.

---

## NFR-004: Background Processing

Long-running scans should not freeze the user interface.

The application should:

- Run scanning tasks in the background
- Update progress continuously
- Keep the dashboard responsive

---

# 2. Reliability Requirements

## NFR-005: Error Recovery

The system should gracefully handle failures.

Supported failure cases:

- Website unavailable
- Timeout
- SSL error
- DNS failure
- Browser crash
- Invalid response

---

## NFR-006: Scan Persistence

Active scan information should be saved.

If the application closes unexpectedly:

The system should preserve:

- Completed results
- Failed results
- Scan history

---

## NFR-007: Data Consistency

Database records must remain accurate.

The system should prevent:

- Duplicate scan records
- Corrupted results
- Invalid states

---

# 3. Database Requirements

## NFR-008: Local Database

The application must use SQLite as the default database.

Benefits:

- No external server required
- Easy deployment
- Local data ownership

---

## NFR-009: Database Backup

The system should allow users to backup database data.

Backup should include:

- Scan history
- Results
- Notes
- Tags
- Settings

---

# 4. Security Requirements

## NFR-010: Local Data Privacy

User data should remain stored locally.

The application should not upload:

- CSV files
- Scan results
- Prospect information

to external services without user permission.

---

## NFR-011: Safe File Handling

Uploaded files should be validated before processing.

The system should check:

- File type
- File size
- File structure

---

## NFR-012: Secure Export

Exported files should only contain user-selected information.

The system should prevent accidental export of unrelated data.

---

# 5. Usability Requirements

## NFR-013: Simple User Interface

The application should be usable without technical knowledge.

The workflow should be:

```
Upload

↓

Scan

↓

Review

↓

Export
```

---

## NFR-014: Clear Feedback

The application should always show current status.

Examples:

```
Scanning 245 / 1000

Completed: 245

Failed: 5
```

---

## NFR-015: Helpful Error Messages

Errors should explain:

- What happened
- Why it happened
- How to fix it

Example:

Bad:

```
Error 500
```

Good:

```
CSV file does not contain a valid domain column.
Please upload a file with website URLs.
```

---

# 6. Maintainability Requirements

## NFR-016: Modular Architecture

The system should separate major components:

```
Frontend

Backend

Scanner

Detection Engine

Database

Export Engine
```

Each module should be independently maintainable.

---

## NFR-017: Clean Code Standards

The codebase should follow:

- Clear naming conventions
- Proper documentation
- Reusable components
- Consistent structure

---

## NFR-018: AI-Friendly Development

The project structure should allow AI coding assistants to understand and modify the system easily.

Requirements:

- Clear documentation
- Small modules
- Descriptive functions
- Defined responsibilities

---

# 7. Scalability Requirements

## NFR-019: Future Expansion

The architecture should support future features.

Possible expansions:

- More detection platforms
- Cloud version
- Team accounts
- CRM integrations
- AI analysis

---

## NFR-020: Detection Engine Expansion

Adding a new tracking technology should not require rewriting the entire system.

Example:

Adding:

```
Snapchat Pixel
```

should only require adding a new detector module.

---

# 8. Compatibility Requirements

## NFR-021: Operating System Support

Initial support:

- Windows
- macOS
- Linux

---

## NFR-022: Browser Compatibility

The application should support:

- Chromium-based scanning

Future:

- Firefox
- WebKit

---

# 9. Resource Management Requirements

## NFR-023: CPU Usage Control

The application should allow users to control scanning intensity.

Example:

```
Low

Medium

High
```

---

## NFR-024: Memory Management

The system should avoid excessive memory usage.

Requirements:

- Close unused browser sessions
- Clean temporary data
- Manage queues efficiently

---

# 10. Logging Requirements

## NFR-025: Application Logging

The system should maintain logs for troubleshooting.

Logs should include:

- Application events
- Scan errors
- Detection issues
- Database errors

---

# Quality Goals Summary

Ads Detector should be:

| Category | Goal |
|---|---|
| Performance | Fast scanning and responsive UI |
| Reliability | Stable long-running scans |
| Security | Local data protection |
| Usability | Simple workflow |
| Maintainability | Modular architecture |
| Scalability | Future-ready design |

---

# Final Requirement

Ads Detector should provide a professional-grade local application experience while remaining simple enough for individual users and agencies to operate without complex infrastructure.
