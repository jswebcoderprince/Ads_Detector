# Functional Overview

## Overview

Ads Detector is a local-first desktop web application built around multiple functional modules working together to scan websites, detect advertising technologies, manage prospects, and generate actionable reports.

This document provides a high-level overview of the application's functional architecture.

Detailed implementation requirements are defined separately in the Functional Requirements section.

---

# Functional Architecture

The application consists of the following major modules:

```
CSV Management

↓

Scan Management

↓

Website Scanner

↓

Detection Engine

↓

Intelligence Engine

↓

Database Layer

↓

Prospect Management

↓

Export System

↓

Dashboard
```

---

# Module Overview

---

# 1. CSV Management Module

## Purpose

Responsible for importing, validating, and preparing website domain data before scanning.

---

## Main Functions

The module handles:

- CSV upload
- File validation
- Domain column detection
- Data cleaning
- Duplicate removal
- Domain normalization
- Scan queue preparation

---

## Input

User uploaded CSV file.

Example:

```
website.com
https://example.com
www.business.com
```

---

## Output

Clean scanning queue:

```
example.com
business.com
```

---

# 2. Scan Management Module

## Purpose

Controls the scanning process and manages scan lifecycle.

---

## Main Functions

The module handles:

- Creating scan sessions
- Managing scan queues
- Tracking progress
- Managing scan status
- Handling retries
- Recording scan completion

---

## Scan States

Possible states:

```
Pending

Running

Completed

Failed

Cancelled
```

---

# 3. Website Scanner Module

## Purpose

Responsible for visiting websites and collecting technical information.

---

## Technology

- Playwright
- Chromium browser

---

## Main Functions

The scanner performs:

- Browser launching
- Website loading
- JavaScript execution
- Network monitoring
- HTML inspection
- Script analysis
- Cookie inspection

---

## Scanner Output

Collected signals:

- Scripts
- Network requests
- Tracking IDs
- Cookies
- Page resources

---

# 4. Detection Engine

## Purpose

Analyzes collected website data and identifies advertising technologies.

---

## Supported Technologies

### Google

- Google Ads
- Conversion Tracking
- Google Tag Manager signals

### Meta

- Meta Pixel

### Microsoft

- Microsoft UET

### TikTok

- TikTok Pixel

### LinkedIn

- LinkedIn Insight Tag

### Pinterest

- Pinterest Tag

---

## Detection Methods

The engine uses:

- HTML analysis
- JavaScript inspection
- Network request monitoring
- Cookie detection

---

# 5. Detection Intelligence Module

## Purpose

Converts raw detection signals into meaningful business insights.

---

## Functions

Generates:

### Detection Status

Example:

```
Detected
Not Detected
Failed
```

---

### Detection Confidence

Levels:

```
High

Medium

Low

None
```

---

### Detection Reason

Example:

```
Google Ads conversion ID detected
```

---

### Detection Method

Example:

```
Network Request
JavaScript
HTML
Cookie
```

---

# 6. Prospect Intelligence Module

## Purpose

Ranks websites based on marketing signals.

---

## Main Functions

The module calculates:

- Prospect Score
- Platform Count
- Marketing Activity Level

---

## Example

```
Domain:

example.com


Detected Platforms:

Google Ads
Meta Pixel


Score:

92/100
```

---

# 7. Database Module

## Purpose

Stores application data locally using SQLite.

---

## Stored Information

### Scan Data

- Scan sessions
- Status
- Duration

---

### Website Results

- Domains
- Detection results
- Confidence
- Scores

---

### User Data

- Notes
- Tags
- Star status
- Settings

---

# 8. Dashboard Module

## Purpose

Provides users with a visual overview of application activity.

---

## Dashboard Information

Displays:

- Total scans
- Total websites processed
- Ads detected
- Average confidence
- Recent activity
- Scan history

---

# 9. Prospect Management Module

## Purpose

Allows users to organize and manage valuable prospects.

---

## Features

Users can:

- Star prospects
- Add notes
- Add tags
- Search prospects
- Filter results
- Sort results

---

## Example Workflow

```
Scan 1000 Websites

↓

Find 200 Qualified Prospects

↓

Star 50 Best Leads

↓

Export 50 Leads
```

---

# 10. Filtering Module

## Purpose

Allows users to narrow large datasets into targeted prospect lists.

---

## Available Filters

### Platform Filters

- Google Ads
- Meta
- TikTok
- LinkedIn
- Microsoft
- Pinterest

---

### Quality Filters

- Confidence Level
- Prospect Score

---

### Status Filters

- Completed
- Failed
- Pending

---

### User Filters

- Starred
- Tagged
- Notes Available

---

# 11. Export Module

## Purpose

Provides flexible data export capabilities.

---

## Export Types

Users can export:

### All Results

Entire scan dataset.

---

### Filtered Results

Only matching filters.

---

### Selected Results

Manually selected websites.

---

### Starred Results

Saved prospects only.

---

### Failed Results

Unsuccessful scans.

---

## Supported Formats

- CSV
- Excel
- JSON

---

# 12. Configuration Module

## Purpose

Manages application settings.

---

## Settings Include

- Scan timeout
- Browser settings
- Concurrency limit
- Export preferences
- Database settings

---

# 13. Error Handling Module

## Purpose

Provides reliable recovery from failures.

---

## Handles

- Invalid CSV
- Website timeout
- SSL errors
- DNS failures
- Browser crashes
- Detection failures

---

# Functional Workflow Summary

The complete application workflow:

```
User Uploads CSV

↓

CSV Validation

↓

Create Scan Session

↓

Generate Scan Queue

↓

Launch Scanner

↓

Collect Website Signals

↓

Run Detection Engine

↓

Generate Intelligence

↓

Store Results

↓

Display Dashboard

↓

Filter Prospects

↓

Export Data
```

---

# Future Functional Expansion

Future versions may include:

- AI website analysis
- Automated recommendations
- CRM integrations
- Cloud synchronization
- Team collaboration
- Scheduled scanning

---

# Summary

Ads Detector is composed of independent but connected modules that work together to transform raw website lists into organized, qualified business intelligence.

The functional architecture is designed to be:

- Modular
- Maintainable
- Scalable
- AI implementation friendly
- Ready for future expansion
