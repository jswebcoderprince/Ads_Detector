# Docker

## Overview

This document describes the Docker-based containerization strategy for Ads Detector, covering how the application, its dependencies, and the Playwright browser automation environment are packaged into reproducible container images for development, testing, and production deployment.

## Purpose

The purpose of this document is to:

- Provide a reproducible, isolated runtime environment for Ads Detector across all deployment targets.
- Eliminate "works on my machine" inconsistencies by standardizing the runtime environment, including browser binaries required by Playwright.
- Simplify onboarding for new developers by reducing local environment setup to a single container build/run step.
- Support the deployment procedures described in `DEPLOYMENT.md`.

## Detailed Explanation

### Container Strategy

Ads Detector uses a multi-stage Docker build to keep the final image lean while ensuring all runtime dependencies — including Playwright's browser binaries — are correctly installed.

**Stage 1 — Build Stage**
- Installs Python dependencies from the project's dependency manifest.
- Installs Playwright and downloads the required browser binaries (Chromium, and any additional browsers configured for scanning).
- Compiles or bundles any frontend assets required by the User Interface module.

**Stage 2 — Runtime Stage**
- Copies only the necessary application code and installed dependencies from the build stage.
- Configures the SQLite database file path as a mounted volume, ensuring data persists across container restarts.
- Sets environment variables consistent with `CONFIGURATION.md`.
- Runs the application as a non-root user for security.

### Base Image Considerations

- The base image must be compatible with Playwright's system-level dependencies (required shared libraries for headless browser execution).
- Official Playwright Docker images are preferred as a base where possible, since they are maintained to match Playwright's browser binary requirements and reduce compatibility issues.

### Volume Mounts

- **Database volume:** the SQLite database file must be mounted from a host volume or named Docker volume to ensure data is not lost when the container is recreated.
- **Export output volume:** the export output directory should be mounted if users need direct host access to generated export files, though in most deployments export files are served via the application's download mechanism instead.

### Networking

- The application exposes a single port for the User Interface and API layer, configurable via `APP_PORT` per `CONFIGURATION.md`.
- Outbound network access must be permitted for the Scanner Engine container/process, since Playwright requires the ability to reach arbitrary external domains during scanning.

## Functional Requirements

- The application must be buildable into a single Docker image using a provided `Dockerfile` at the project root.
- The container must run the application successfully with only environment variables and a mounted database volume as required inputs.
- Container startup must fail fast and clearly if required configuration or the Playwright browser binaries are missing.

## Technical Considerations

- Playwright's browser binaries are large and version-sensitive; the Docker image must pin the Playwright package version and corresponding browser binary version together to avoid mismatches between the installed library and downloaded browsers.
- Because the Scanner Engine spawns browser processes, the container must be allocated sufficient memory and CPU resources; resource limits configured too conservatively will cause scan timeouts or browser crashes.
- SQLite, as a file-based database, requires careful volume configuration in containerized environments to avoid file locking issues if multiple container instances attempt to write to the same database file concurrently.

## Workflow / Process

```
Dockerfile Defined (Multi-Stage Build)
              ↓
Build Stage: Install Dependencies + Playwright Browsers
              ↓
Runtime Stage: Copy Application + Dependencies
              ↓
Image Built and Tagged
              ↓
Container Run with Mounted Volumes and Environment Variables
              ↓
Application Starts and Validates Configuration
              ↓
Container Ready to Accept Scan Requests
```

## Error Handling

- If the Playwright browser binaries fail to install during the build stage, the build must fail immediately with a clear error rather than producing an image that fails at scan time.
- If the mounted database volume is not writable at container startup, the application must fail fast with a descriptive permissions error.
- Container health checks must be configured to detect and report a non-responsive application process, enabling orchestration platforms to restart unhealthy containers.

## Security Considerations

- The container must run the application process as a non-root user to limit the impact of a potential compromise.
- Base images must be kept up to date with security patches; the Docker build should be rebuilt periodically even without application code changes to pick up base image security updates.
- Secrets must never be baked into the Docker image at build time; all secrets must be supplied at runtime via environment variables or a secrets manager, per `CONFIGURATION.md`.
- Outbound scanning traffic from the container should be monitored, since the Scanner Engine intentionally initiates connections to arbitrary external domains.

## Future Improvements

- Introduce a `docker-compose.yml` for local development that wires together the application container, volume mounts, and any auxiliary services in a single command.
- Add multi-architecture image builds (e.g., `linux/amd64` and `linux/arm64`) to support a broader range of deployment hosts.
- Explore a distroless or minimal base image variant to further reduce image size and attack surface once Playwright compatibility is confirmed.
- Add automated container image vulnerability scanning as part of the CI pipeline.

## Summary

The Docker containerization strategy packages Ads Detector, its Python dependencies, and the Playwright browser automation environment into a reproducible, multi-stage container image. This ensures consistent behavior across development, testing, and production, while addressing the specific operational needs of a browser-automation-driven scanning workload, including resource allocation, volume persistence for the SQLite database, and secure, non-root execution.
