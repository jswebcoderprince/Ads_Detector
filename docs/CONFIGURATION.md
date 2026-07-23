# Configuration

## Overview

This document describes the configuration system used by Ads Detector, including how application settings, environment variables, scanner parameters, detection rule configuration, and database connection details are defined, loaded, and managed across development, testing, and production environments.

## Purpose

The purpose of this document is to:

- Define all configurable parameters that control the behavior of Ads Detector.
- Establish a clear separation between code and environment-specific settings.
- Provide a reference for developers and operators setting up the application in different environments.
- Ensure configuration practices align with the security and deployment requirements described in `SECURITY.md` and `DEPLOYMENT.md`.

## Detailed Explanation

### Configuration Sources

Ads Detector loads configuration from the following sources, in order of precedence (highest to lowest):

1. **Environment variables** — used for secrets, deployment-specific overrides, and environment identification.
2. **Local configuration file** (`config.local.yaml` or `.env`) — used for developer-specific overrides, excluded from version control.
3. **Default configuration file** (`config.default.yaml`) — checked into version control, providing sane defaults for local development.

### Core Configuration Categories

**Application Settings**
- `APP_ENV` — current environment (`development`, `testing`, `production`).
- `APP_LOG_LEVEL` — logging verbosity, consistent with `LOGGING.md`.
- `APP_PORT` — port the application listens on, if applicable.

**Database Settings**
- `DATABASE_PATH` — path to the SQLite database file for the current environment.
- `DATABASE_BACKUP_DIR` — directory used for automated database backups.

**Scanner Engine Settings**
- `SCANNER_MAX_CONCURRENT_SCANS` — maximum number of simultaneous Playwright browser instances.
- `SCANNER_TIMEOUT_SECONDS` — maximum time allowed per domain scan before it is marked as timed out.
- `SCANNER_MAX_REDIRECTS` — maximum redirect chain depth followed per domain.
- `SCANNER_USER_AGENT` — user agent string presented by the automated browser during scans.
- `SCANNER_ALLOW_HTTP_FALLBACK` — whether to retry a failed `https://` navigation over `http://` (see reference below).

**Detection Engine Settings**
- `DETECTION_RULESET_PATH` — path to the versioned detection rule definitions.
- `DETECTION_CONFIDENCE_HIGH_THRESHOLD` — lowest score labelled **High** confidence (see reference below).
- `DETECTION_CONFIDENCE_MEDIUM_THRESHOLD` — lowest score labelled **Medium** confidence (see reference below).

**CSV Processing Settings**
- `CSV_MAX_FILE_SIZE_MB` — maximum accepted upload size.
- `CSV_MAX_ROWS` — maximum number of domain rows processed per upload.

**Export Settings**
- `EXPORT_MAX_ROWS` — maximum number of rows permitted in a single export operation.
- `EXPORT_OUTPUT_DIR` — directory where generated export files are temporarily stored before download.

### Detailed Parameter Reference

The parameters below control detection scoring and scanner navigation behavior. All three are read through the centralized configuration object and can be changed without any code change.

#### `DETECTION_CONFIDENCE_HIGH_THRESHOLD`

- **Purpose:** The lowest confidence score that is labelled **High**. Together with `DETECTION_CONFIDENCE_MEDIUM_THRESHOLD`, it defines the numeric-to-categorical mapping (High / Medium / Low) applied to every detection, as specified in `CONFIDENCE_SCORING.md`. This satisfies the requirement that confidence bands be configurable without code changes.
- **Default value:** `80`
- **Allowed values:** An integer from `1` to `100`. Must be **greater than** `DETECTION_CONFIDENCE_MEDIUM_THRESHOLD`. Scores at or above this value are labelled High; the combined constraint is `1 ≤ MEDIUM < HIGH ≤ 100`.
- **Notes:** The canonical bands are defined by `FR-008_CONFIDENCE_SCORING.md` (the single source of truth): High 80–100, Medium 50–79, Low 20–49. An invalid value (out of range, or not greater than the medium threshold) is rejected at startup rather than during a scan.

#### `DETECTION_CONFIDENCE_MEDIUM_THRESHOLD`

- **Purpose:** The lowest confidence score that is labelled **Medium**. Scores at or above this value but below `DETECTION_CONFIDENCE_HIGH_THRESHOLD` are Medium; scores below it (down to 1) are Low. A score of `0` is reserved for "not detected" and is never stored as a detection.
- **Default value:** `50`
- **Allowed values:** An integer from `1` to `100`. Must be **less than** `DETECTION_CONFIDENCE_HIGH_THRESHOLD` (i.e. `1 ≤ MEDIUM < HIGH ≤ 100`).
- **Notes:** Because every detected technology scores at least `1`, scores of `1–19` fall below the canonical Low band's lower bound of `20` but are still shown as Low — there is no "detected but None" state.

#### `SCANNER_ALLOW_HTTP_FALLBACK`

- **Purpose:** Controls whether the Scanner Engine retries a domain over `http://` when the initial `https://` navigation fails at the connection level (DNS failure, connection refused, TLS error). This lets the scanner reach sites that are not served over HTTPS while still preferring HTTPS first. A **timeout** is never retried over `http://`, since a reachable-but-slow site would likely time out again; only connection-level failures trigger the fallback.
- **Default value:** `true`
- **Allowed values:** A boolean. Accepted true forms: `true`, `1`, `yes`, `on`; any other value (e.g. `false`, `0`, `no`, `off`) is treated as false. Parsing is case-insensitive. If the key is absent, it defaults to `true`.
- **Notes:** This parameter is optional; omitting it preserves the default behavior.

### Configuration Validation

- On application startup, all required configuration values are validated for presence and type correctness.
- Missing required configuration values must halt application startup with a descriptive error rather than allowing the application to run with undefined behavior.
- Confidence threshold values are validated to satisfy `1 ≤ DETECTION_CONFIDENCE_MEDIUM_THRESHOLD < DETECTION_CONFIDENCE_HIGH_THRESHOLD ≤ 100`; a violation halts startup.

### Example Configuration

The following shows these parameters in `config.default.yaml` (checked-in defaults) and as environment-variable overrides.

**`config.default.yaml`:**

```yaml
# Detection Engine
DETECTION_RULESET_PATH: src/detection/rules
DETECTION_CONFIDENCE_HIGH_THRESHOLD: 80
DETECTION_CONFIDENCE_MEDIUM_THRESHOLD: 50

# Scanner Engine
SCANNER_ALLOW_HTTP_FALLBACK: true
```

**Environment-variable overrides (highest precedence):**

```bash
# Require stronger evidence before labelling a detection High/Medium
export DETECTION_CONFIDENCE_HIGH_THRESHOLD=90
export DETECTION_CONFIDENCE_MEDIUM_THRESHOLD=60

# Only ever scan over HTTPS; never fall back to http://
export SCANNER_ALLOW_HTTP_FALLBACK=false
```

## Functional Requirements

- All configurable parameters must have documented defaults suitable for local development.
- Production deployments must override all secrets and environment-specific values via environment variables, never via checked-in files.
- Configuration changes must not require code changes or redeployment of application logic — only a configuration reload or restart.
- The system must expose a way to view currently active (non-secret) configuration values for debugging purposes.

## Technical Considerations

- Configuration loading must occur once at application startup and be exposed through a centralized configuration object accessible to all modules (CSV Processor, Scanner Engine, Detection Engine, Database Layer, Export System, User Interface), rather than each module reading environment variables independently.
- Scanner Engine configuration must account for the resource intensity of Playwright browser automation; concurrency settings should be tunable based on host machine capability.
- Detection rule configuration must support versioning so that historical scan results can be traced back to the ruleset version active at the time of the scan.

## Workflow / Process

```
Application Startup
        ↓
Load Default Configuration File
        ↓
Overlay Local Configuration File (if present)
        ↓
Overlay Environment Variables (highest precedence)
        ↓
Validate Required Values
        ↓
Expose Centralized Configuration Object to All Modules
```

## Error Handling

- Missing required configuration values must produce a clear startup error identifying the missing key and expected type.
- Invalid configuration values (e.g., non-numeric timeout, negative concurrency limit) must be rejected at startup rather than causing runtime failures during scanning.
- Configuration reload failures in a running instance must not crash the application; the system must continue operating on the last known valid configuration and log the reload failure.

## Security Considerations

- Secrets (database credentials if applicable, API keys for optional integrations) must never be committed to version control; `.env` and `config.local.yaml` must be included in `.gitignore`.
- Configuration values exposed for debugging must redact any sensitive fields (e.g., masked credentials) rather than displaying raw secret values.
- File system paths defined in configuration (database path, export output directory) must be validated to prevent path traversal when combined with user-influenced input.

## Future Improvements

- Introduce a schema-based configuration validation library to formalize type and range checks.
- Support hot-reloading of non-critical configuration values (e.g., logging level) without requiring application restart.
- Add a configuration management UI for administrators to adjust scanner and detection parameters without direct file access.
- Support environment-specific configuration profiles for multi-tenant or multi-instance deployments if the platform expands beyond single-user/local deployment.

## Summary

The configuration system provides a structured, layered approach to managing application settings across environments, ensuring that Ads Detector behaves predictably in development, testing, and production while keeping secrets and environment-specific values properly separated from source code, consistent with the project's security and deployment practices.
