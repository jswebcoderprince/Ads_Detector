# Playwright Engine

## Overview

This document describes the implementation details of the Playwright-based browser automation layer that powers the Website Scanner module within Ads Detector. Playwright is the chosen automation framework responsible for loading target websites in a real browser context, capturing network activity, and exposing the data required by the Detection Engine.

## Purpose

The purpose of this document is to:

- Document why Playwright was selected as the browser automation technology for Ads Detector.
- Describe how Playwright is configured and operated within the Scanner Engine.
- Define the specific data captured during a Playwright-driven scan session.
- Provide technical guidance for maintaining and extending the scanning implementation.

## Detailed Explanation

### Why Playwright

Playwright was selected over alternative browser automation tools for the following reasons:

- **Full browser rendering.** Many advertising, tracking, and analytics technologies are injected via JavaScript after initial page load; a real rendering engine is required to observe their actual runtime behavior, which simple HTTP-request-based scraping cannot capture.
- **Network interception.** Playwright provides first-class APIs for intercepting and inspecting all network requests and responses made by a page, which is essential for detecting ad server calls, tracking pixel beacons, and analytics requests.
- **Multi-browser support.** Playwright supports Chromium, Firefox, and WebKit engines, allowing the Scanner Engine to validate detection consistency across rendering engines if needed.
- **Modern async API.** Playwright's asynchronous API model aligns well with the concurrency requirements of scanning many domains efficiently.

### Scanner Configuration

- The Scanner Engine launches a Playwright browser instance (Chromium by default) in headless mode for each scan, or reuses a pooled browser context depending on the configured concurrency strategy.
- Each scan navigates to the target domain's root URL using the `https://` protocol by default, falling back to `http://` if the secure connection fails, consistent with domain normalization rules.
- A configurable navigation timeout (`SCANNER_TIMEOUT_SECONDS`) bounds how long the engine waits for the page to reach a stable load state.
- A custom user agent string (`SCANNER_USER_AGENT`) is set to identify the scanner's requests appropriately and avoid being blocked by basic bot-detection mechanisms unnecessarily.

### Captured Data

For each scanned domain, the Playwright Engine captures:

- **All outbound network requests**, including URL, method, request headers, and initiator information.
- **All response headers** for each request, including Set-Cookie headers.
- **Cookies set** during the page session.
- **The final rendered DOM**, including dynamically injected script tags and iframes.
- **Redirect chains**, recording each hop up to the configured maximum redirect depth.
- **Console errors and page-level exceptions**, useful for diagnosing scan reliability issues distinct from detection logic.

### Handling Real-World Website Behavior

- **Lazy-loaded content:** the engine waits for a configurable network-idle period before considering the page fully loaded, to capture technologies that load asynchronously after initial render.
- **Pop-ups and consent banners:** the engine does not attempt to interact with cookie consent banners or pop-ups by default, since detection is based on technologies present regardless of user interaction state; this behavior may be revisited if consent-gated tracking becomes a significant blind spot.
- **CAPTCHA and bot-detection walls:** when the engine detects a CAPTCHA challenge or an explicit bot-blocking response, the scan is marked as "blocked" rather than producing a false negative for technology detection.

## Functional Requirements

- The Playwright Engine must capture all network requests, response headers, cookies, and DOM content required by the Detection Engine for every successfully completed scan.
- The engine must respect the configured per-domain timeout and never allow a single unresponsive domain to block the overall scan queue.
- The engine must record distinct, identifiable outcomes for successful scans, timeouts, redirects, and blocked/CAPTCHA responses.

## Technical Considerations

- Browser instance lifecycle management (launching, reusing, and closing browser contexts) must balance scan throughput against memory consumption, since each active browser context consumes significant system resources.
- The engine must isolate each scan within its own browser context (not just a new tab) to prevent cookies, local storage, or cached state from one domain leaking into the scan of another domain.
- Network request capture must be structured in a format directly consumable by the Detection Engine's rule-matching logic, avoiding the need for the Detection Engine to re-parse raw Playwright event objects.
- Because Playwright drives a real browser, the engine is subject to the same rendering quirks and inconsistencies as real-world browsing; detection logic must account for minor variability in request timing and ordering across scans of the same domain.

## Workflow / Process

```
Scan Queue Provides Next Domain
              ↓
Playwright Browser Context Launched (or Reused from Pool)
              ↓
Navigation to Target Domain Initiated
              ↓
Network Requests, Responses, Cookies, and DOM Captured
              ↓
Network-Idle / Timeout Condition Reached
              ↓
Captured Scan Data Packaged and Passed to Detection Engine
              ↓
Browser Context Closed or Returned to Pool
```

## Error Handling

- Navigation failures (DNS resolution errors, connection refused, SSL errors) must be caught and recorded as a distinct scan outcome rather than allowed to propagate as unhandled exceptions.
- Timeout errors must result in the domain being marked as "timeout" in the scan results, with partial data (if any was captured before the timeout) preserved for diagnostic purposes.
- Unexpected Playwright runtime errors (e.g., browser crash) must trigger a retry with a fresh browser context up to a configured retry limit before the domain is marked as failed.

## Security Considerations

- Each scan must run in an isolated browser context to prevent cross-domain data leakage and to ensure that a malicious or compromised target site cannot affect the scanning of subsequent domains.
- The Playwright Engine must run browsers in a sandboxed environment; scanned websites must never be able to execute code outside the browser sandbox or access the host file system.
- Downloads, file system prompts, and native dialogs triggered by scanned websites must be automatically dismissed or blocked to prevent unintended file system interaction during automated scanning.

## Future Improvements

- Add support for scanning with multiple browser engines (Firefox, WebKit) to detect technologies that behave differently across rendering engines.
- Introduce a browser context pooling strategy to reduce the overhead of repeatedly launching new browser instances for high-volume scan sessions.
- Evaluate optional interaction simulation (e.g., dismissing cookie consent banners) to assess whether consent-gated tracking technologies should be included in detection scope.
- Add mobile viewport emulation to detect technologies that only activate on mobile-rendered versions of a site.

## Summary

The Playwright Engine is the technical foundation of the Website Scanner module, providing full browser rendering and network interception capabilities necessary to observe real-world advertising, tracking, and analytics behavior on scanned websites. Its configuration balances scan accuracy, throughput, and resource consumption, while its isolation and sandboxing practices ensure that scanning arbitrary third-party websites remains safe and reliable.
