# Ads Detector

> Enterprise-grade local web application for detecting advertising
> technologies across websites using Playwright.

------------------------------------------------------------------------

# Overview

Ads Detector is a local web application designed for agencies,
marketers, researchers, and sales teams who need to determine whether
websites are actively using online advertising technologies.

The application accepts a CSV file containing website domains and
automatically scans each website using a real Chromium browser powered
by Playwright.

Unlike simple HTML scrapers, Ads Detector renders JavaScript before
analyzing the page, allowing detection of dynamically loaded advertising
technologies.

The application focuses exclusively on detecting advertising
technologies.

Supported platforms:

-   Google Ads
-   Google Remarketing
-   Meta Pixel
-   Microsoft UET
-   TikTok Pixel
-   LinkedIn Insight Tag
-   Pinterest Tag

------------------------------------------------------------------------

# Project Goals

-   Upload a CSV containing domains.
-   Automatically identify the domain column.
-   Scan websites using Playwright.
-   Execute JavaScript before detection.
-   Detect supported advertising technologies.
-   Continue scanning even if websites fail.
-   Export a CSV report.
-   Run entirely on the user's local computer.

------------------------------------------------------------------------

# Target Users

-   Digital Agencies
-   Cold Email Agencies
-   Lead Generation Teams
-   Marketing Consultants
-   PPC Specialists
-   Growth Agencies
-   Researchers

------------------------------------------------------------------------

# Project Scope

## Included

-   CSV Upload
-   Automatic Domain Detection
-   Playwright Browser Automation
-   Parallel Website Scanning
-   Advertising Technology Detection
-   Progress Tracking
-   CSV Export
-   Local Web Application

## Excluded

-   SEO Audit
-   Performance Analysis
-   AI Features
-   CRM
-   Contact Extraction
-   Authentication
-   Database

------------------------------------------------------------------------

# Supported Advertising Platforms

  Platform             Supported
  -------------------- -----------
  Google Ads           ✅
  Google Remarketing   ✅
  Meta Pixel           ✅
  Microsoft UET        ✅
  TikTok Pixel         ✅
  LinkedIn Insight     ✅
  Pinterest Tag        ✅

------------------------------------------------------------------------

# High-Level Workflow

``` text
Upload CSV
    ↓
Validate CSV
    ↓
Detect Domain Column
    ↓
Create Scan Queue
    ↓
Launch Playwright Workers
    ↓
Render Website
    ↓
Run Detection Engine
    ↓
Store Results
    ↓
Export CSV
```

------------------------------------------------------------------------

# Technology Stack

## Frontend

-   React
-   Vite
-   Tailwind CSS

## Backend

-   Python
-   FastAPI

## Browser Automation

-   Playwright Chromium

## CSV Processing

-   Pandas

------------------------------------------------------------------------

# Repository Structure

``` text
ads-detector-docs/
├── README.md
├── PRODUCT_VISION.md
├── PROJECT_SCOPE.md
├── FUNCTIONAL_REQUIREMENTS.md
├── SYSTEM_ARCHITECTURE.md
├── API_SPECIFICATION.md
├── SCANNER_ENGINE.md
├── DETECTION_ENGINE.md
├── PLAYWRIGHT_ENGINE.md
├── CODING_STANDARDS.md
└── AI_IMPLEMENTATION_RULES.md
```

------------------------------------------------------------------------

# Design Philosophy

-   Keep the application focused.
-   Prefer reliability over feature count.
-   Use real browser rendering.
-   Modular architecture.
-   Maintainable codebase.
-   Production-ready implementation.

------------------------------------------------------------------------

# Success Criteria

-   Scan large CSV files reliably.
-   Detect supported advertising technologies.
-   Continue when individual websites fail.
-   Export clean CSV reports.
-   Maintain responsive UI.

------------------------------------------------------------------------

# Version

**Version:** 1.0.0 (Documentation)

**Status:** In Development

------------------------------------------------------------------------

# License

Private Project

------------------------------------------------------------------------

# Next Document

**PRODUCT_VISION.md**
