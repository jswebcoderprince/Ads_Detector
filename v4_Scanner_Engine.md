# Ads Detector PRD v4 - Scanner Engine

## Browser

-   Playwright Chromium
-   Headless mode
-   One browser instance
-   One context per domain

## Scan Flow

1.  Normalize domain
2.  Open homepage
3.  Wait for network idle
4.  Capture HTML + scripts
5.  Inspect network requests
6.  Run detectors
7.  Save result
8.  Close context

## Retry

-   Retry once after timeout
-   Log failure reason

## Concurrency

-   Default: 5 workers
-   Configurable
