# Logging

## Overview

This document defines the logging strategy for Ads Detector, describing what events are logged, at what severity level, in what format, and how logs support debugging, monitoring, and auditability across the CSV Processor, Scanner Engine, Detection Engine, Database Layer, Export System, and User Interface modules.

## Purpose

The purpose of this document is to:

- Establish a consistent logging approach across all modules of the application.
- Ensure that failures, especially in the Scanner Engine and Detection Engine, are traceable and debuggable after the fact.
- Support operational visibility into scan queue throughput, error rates, and system health.
- Align logging practices with the error handling conventions described in `ERROR_HANDLING.md`.

## Detailed Explanation

### Log Levels

Ads Detector uses standard, ordered log severity levels:

- **DEBUG** — Detailed diagnostic information useful only during active development or troubleshooting (e.g., raw evidence match details).
- **INFO** — Normal operational events (e.g., "scan started for domain X", "CSV upload validated, 120 valid rows").
- **WARNING** — Recoverable or non-critical issues (e.g., a domain timed out but the scan queue continues, a CSV row was skipped due to a malformed value).
- **ERROR** — Failures that prevent a specific operation from completing (e.g., a scan crashed, a database write failed).
- **CRITICAL** — Failures that threaten the stability of the entire application (e.g., database connection lost, configuration failed to load at startup).

### Structured Logging

- All log entries must be structured (e.g., JSON-formatted) rather than free-form text, to support automated parsing, filtering, and future log aggregation tooling.
- Each log entry must include, at minimum:
  - Timestamp (ISO 8601 format)
  - Log level
  - Module/component name (e.g., `scanner_engine`, `detection_engine`, `csv_processor`)
  - Message
  - Relevant contextual identifiers (e.g., `domain`, `scan_session_id`, `scan_id`)

### Module-Specific Logging Expectations

**CSV Processor**
- Logs upload receipt, validation summary (valid/invalid/duplicate counts), and any parsing errors.

**Scanner Engine**
- Logs scan start, scan completion, timeouts, redirects followed, and blocked/CAPTCHA outcomes, each tagged with the domain and scan session ID.

**Detection Engine**
- Logs which detection rules matched per domain at DEBUG level; logs detection summary counts at INFO level.

**Confidence Scoring**
- Logs final scores per domain/technology at INFO level; logs configuration or calculation errors at ERROR level.

**Database Layer**
- Logs write successes at DEBUG level (to avoid excessive volume) and all write failures or transaction rollbacks at ERROR level.

**Export System**
- Logs export requests, the active filter criteria used, row counts exported, and any generation failures.

**User Interface**
- Logs user-initiated actions relevant to auditability (e.g., star/unstar, tag changes, export triggered), without logging sensitive free-text note content at levels above DEBUG.

## Functional Requirements

- Every module must emit structured logs consistent with the format defined in this document.
- Log level must be configurable via the `APP_LOG_LEVEL` setting described in `CONFIGURATION.md`, without requiring a code change.
- Critical failures (CRITICAL level) must be logged in a way that is guaranteed to be flushed to persistent storage even if the application crashes immediately afterward.

## Technical Considerations

- Because the Scanner Engine operates with concurrent Playwright browser instances, log entries must include enough contextual identifiers (domain, scan session ID) to allow logs from concurrent scans to be disambiguated during review.
- Logging must not become a performance bottleneck; DEBUG-level logging that captures large payloads (e.g., full DOM snapshots) must be gated behind explicit configuration and disabled by default in production.
- Log output destinations (console, file, or external log aggregation service) must be configurable independently of log level.

## Workflow / Process

```
Event Occurs in a Module
              ↓
Log Entry Constructed with Level, Context, and Message
              ↓
Log Level Checked Against Configured Threshold
              ↓
Entry Emitted to Configured Output (Console / File / Aggregator)
              ↓
Logs Available for Debugging, Monitoring, and Audit Review
```

## Error Handling

- Logging failures themselves (e.g., inability to write to a log file) must not crash the application; such failures should fall back to a safe default output (e.g., stderr) and be surfaced as a CRITICAL-level warning if possible.
- Errors already captured and handled per `ERROR_HANDLING.md` must always be logged with sufficient context to diagnose the root cause without needing to reproduce the failure.

## Security Considerations

- Logs must never include secrets, credentials, or full contents of configuration values marked as sensitive.
- User-supplied free-text fields (notes) should be logged only at DEBUG level, if at all, and must be treated as untrusted content when included in log entries to prevent log injection.
- Access to production log files or log aggregation dashboards must be restricted to authorized personnel only.

## Future Improvements

- Integrate with a centralized log aggregation and search platform (e.g., ELK stack or equivalent) as the deployment scale grows beyond single-instance/local usage.
- Add correlation IDs that span an entire scan session end-to-end, from CSV upload through export, to simplify cross-module tracing.
- Introduce automated alerting rules based on ERROR/CRITICAL log volume thresholds.
- Add log retention and rotation policies to manage disk usage in long-running deployments.

## Summary

The logging strategy for Ads Detector establishes structured, leveled logging across every module, ensuring that scan failures, detection issues, and system errors are traceable and diagnosable. By standardizing log format and contextual fields, the system supports effective debugging during development and reliable operational monitoring in production.
