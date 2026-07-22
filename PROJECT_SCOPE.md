# PROJECT_SCOPE.md

# Project Scope

**Project:** Ads Detector

**Version:** 1.0

**Status:** Approved

---

# Purpose

This document defines the exact scope of Version 1.

Every implementation must follow this document.

Features outside this scope must NOT be implemented unless the project owner explicitly approves them.

---

# Primary Objective

Build a local web application that allows users to upload a CSV file containing website domains and automatically determine whether those websites appear to use supported advertising technologies.

The application is designed for one task only:

> Detect advertising technologies on websites.

---

# In Scope

## CSV Upload

The application shall support uploading CSV files from the local computer.

Supported examples:

```csv
domain
google.com
nike.com
tesla.com
```

```csv
website
https://google.com
https://nike.com
```

```csv
Company,Website
Google,google.com
Nike,nike.com
```

The application must automatically detect the website/domain column.

---

## Website Scanning

The application shall:

- Normalize domains
- Validate URLs
- Open websites using Playwright
- Wait for JavaScript execution
- Inspect rendered content
- Inspect loaded scripts
- Inspect network requests
- Return scan results

---

## Supported Detection

Version 1 shall detect:

| Technology | Required |
|------------|----------|
| Google Ads | Yes |
| Google Remarketing | Yes |
| Meta Pixel | Yes |
| Microsoft UET | Yes |
| TikTok Pixel | Yes |
| LinkedIn Insight | Yes |
| Pinterest Tag | Yes |

No additional advertising platforms shall be included.

---

## Progress Tracking

The interface shall display:

- Total websites
- Completed
- Remaining
- Failed
- Current website being scanned

---

## Results

Each scanned website shall produce one result.

Required output:

| Column |
|----------|
| Domain |
| Status |
| Google Ads |
| Google Remarketing |
| Meta Pixel |
| Microsoft UET |
| TikTok Pixel |
| LinkedIn Insight |
| Pinterest |
| Result |
| Scan Time |

---

## Export

The application shall export results as CSV.

The exported CSV shall preserve the original row order.

---

# Out of Scope

The following features are intentionally excluded.

## SEO

- Meta Title
- Meta Description
- Robots
- Sitemap
- Lighthouse
- SEO Score

---

## Website Performance

- PageSpeed
- Core Web Vitals
- CLS
- LCP
- INP
- FCP

---

## Marketing Analysis

- Contact Extraction
- Lead Score
- Opportunity Score
- AI Audit
- AI Recommendations

---

## CRM

- HubSpot
- Salesforce
- Pipedrive
- Zoho

---

## Authentication

- Login
- Registration
- Teams
- Permissions

---

## Database

Version 1 shall not require a database.

All processing is temporary and in-memory.

---

## Cloud Features

Version 1 shall NOT include:

- Cloud storage
- Online accounts
- Remote sync
- SaaS deployment

The application must operate locally.

---

# Functional Limits

Version 1 should support:

- CSV Upload
- Local processing
- Browser rendering
- CSV export

No additional business workflows shall be implemented.

---

# Design Constraints

The implementation must use:

Frontend

- React
- Vite
- TailwindCSS

Backend

- FastAPI

Browser

- Playwright Chromium

Python Version

- 3.12+

---

# Success Criteria

Version 1 is complete when the application can:

- Upload CSV
- Detect domains
- Scan websites
- Detect supported advertising technologies
- Show progress
- Export results

No additional functionality is required.

---

# Change Management

Any feature outside this document must be considered a Version 2 request.

Version 1 scope must remain stable.

---

# Approval

This document acts as the official scope definition for the Ads Detector project.

Future implementation must follow this specification exactly.
