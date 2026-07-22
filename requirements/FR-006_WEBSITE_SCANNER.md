# FR-006: Website Scanner

## Requirement ID

FR-006

---

## Requirement Name

Automated Website Scanning Engine

---

# Purpose

The Website Scanner module is responsible for automatically visiting websites, loading their content, collecting technical signals, and preparing data for advertising technology detection.

The scanner acts as the data collection layer between the website and the Detection Engine.

---

# Related User Stories

- US-004: Start Website Scan
- US-005: Monitor Scan Progress
- US-006: Handle Failed Websites
- US-007: Detect Advertising Technologies

---

# Functional Description

The system shall use browser automation technology to open websites and collect information required for advertising technology detection.

Technology:

```
Playwright
+
Chromium Browser
```

---

# Scanner Workflow

```
Receive Domain

↓

Launch Browser Context

↓

Navigate Website

↓

Wait For Page Load

↓

Execute JavaScript

↓

Monitor Network Activity

↓

Collect Website Signals

↓

Send Data To Detection Engine

↓

Store Results
```

---

# Browser Management

The scanner should create isolated browser sessions.

Each website scan should have:

- Separate browser context
- Independent cookies
- Independent storage
- Clean environment

---

# Website Loading

The scanner should support:

## HTTPS Websites

Example:

```
https://example.com
```

---

## HTTP Websites

Example:

```
http://example.com
```

---

# Page Loading Behavior

The scanner should:

- Open website URL
- Wait for page response
- Execute JavaScript
- Allow tracking scripts to load
- Capture required signals

---

# Loading Strategy

The scanner should support configurable loading timeout.

Default:

```
30 seconds
```

Example:

```
Website loads within 30 seconds

↓

Continue scanning


Website exceeds timeout

↓

Mark as failed
```

---

# Data Collection

During scanning, the system should collect:

---

## HTML Data

Including:

- Page source
- Script tags
- Meta information

---

## JavaScript Data

Including:

- Loaded scripts
- Tracking libraries
- Pixel initialization code

---

## Network Data

Including:

- External requests
- Tracking endpoints
- Advertising requests

---

## Cookie Data

Including:

- Tracking cookies
- Marketing cookies
- Third-party cookies

---

# Collected Signals

Example:

```
Script:

googletagmanager.com


Network:

googleadservices.com


Cookie:

_fbp
```

---

# Dynamic Website Support

The scanner must support JavaScript-rendered websites.

Examples:

- React websites
- Vue websites
- Angular websites
- WordPress websites
- E-commerce websites

---

# Browser Configuration

The scanner should support:

## User Agent

Default:

```
Modern Chrome Browser
```

---

## JavaScript

Enabled:

```
YES
```

---

## Cookies

Enabled:

```
YES
```

---

# Resource Control

The scanner should manage resources efficiently.

Requirements:

- Close browser after scan
- Release memory
- Avoid unlimited browser sessions
- Control concurrency

---

# Scan Status Updates

During scanning, the system should provide:

Example:

```
Currently Scanning:

example.com


Status:

Loading Website
```

Possible states:

```
Starting

Loading

Collecting Data

Analyzing

Completed

Failed
```

---

# Error Handling

The scanner should handle:

---

## Website Timeout

Example:

```
Website did not respond within timeout period.
```

Status:

```
Failed
```

---

## DNS Error

Example:

```
Domain could not be resolved.
```

---

## SSL Error

Example:

```
Secure connection failed.
```

---

## Browser Error

Example:

```
Browser session crashed.
Retry available.
```

---

## Blocked Website

Example:

```
Website blocked automated access.
```

---

# Failed Scan Behavior

A failed website should:

- Save failure reason
- Update queue status
- Allow retry
- Continue remaining scans

---

# Database Storage

Scanner results should store:

## Scan Information

```
scan_id

domain

status

duration

error_message
```

---

## Technical Data

```
html_data

scripts_found

network_requests

cookies_found
```

---

# Performance Requirements

The scanner should:

- Support 1000+ websites
- Use controlled concurrency
- Avoid excessive memory usage
- Maintain stable operation during long scans

---

# Security Requirements

The scanner should:

- Run websites in isolated contexts
- Prevent local system access
- Avoid downloading unnecessary files
- Limit browser permissions

---

# Acceptance Criteria

The feature is complete when:

## AC-001

System can automatically open websites.

---

## AC-002

System can collect HTML, JavaScript, and network signals.

---

## AC-003

System supports JavaScript-heavy websites.

---

## AC-004

System handles website failures gracefully.

---

## AC-005

System sends collected data to Detection Engine.

---

## AC-006

Scanner updates scan progress correctly.

---

# Future Improvements

Possible enhancements:

- Browser fingerprint rotation
- Multiple browser engines
- Screenshot capture
- Website performance analysis
- Mobile device simulation

---

# Summary

FR-006 defines the core website scanning capability of Ads Detector.

The Website Scanner converts websites into structured technical data that can be analyzed by the Detection Engine to identify advertising technologies and marketing signals.
