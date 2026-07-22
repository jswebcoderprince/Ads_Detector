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

**Detection Engine Settings**
- `DETECTION_RULESET_PATH` — path to the versioned detection rule definitions.
- `DETECTION_CONFIDENCE_THRESHOLDS` — thresholds mapping numeric scores to High/Medium/Low labels, per `CONFIDENCE_SCORING.md`.

**CSV Processing Settings**
- `CSV_MAX_FILE_SIZE_MB` — maximum accepted upload size.
- `CSV_MAX_ROWS` — maximum number of domain rows processed per upload.

**Export Settings**
- `EXPORT_MAX_ROWS` — maximum number of rows permitted in a single export operation.
- `EXPORT_OUTPUT_DIR` — directory where generated export files are temporarily stored before download.

### Configuration Validation

- On application startup, all required configuration values are validated for presence and type correctness.
- Missing required configuration values must halt application startup with a descriptive error rather than allowing the application to run with undefined behavior.

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
