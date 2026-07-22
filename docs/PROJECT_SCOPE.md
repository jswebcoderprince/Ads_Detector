# Project Scope

## Overview

Ads Detector is a local-first desktop web application designed to scan website domains, detect advertising technologies, analyze marketing signals, and organize qualified prospects.

This document defines the boundaries of the project, including what features are included, excluded, and planned for future versions.

---

# Project Goals

The primary goal of Ads Detector is to create a reliable advertising technology detection and prospect intelligence tool that allows users to:

- Scan multiple websites automatically
- Detect advertising platforms
- Analyze detection confidence
- Organize prospects
- Export qualified results

---

# Version 1 Scope

Version 1 focuses on creating a complete local desktop web application.

The application will provide the following capabilities:

---

# 1. CSV Management Module

## Included

Users can:

- Upload CSV files
- Validate CSV structure
- Detect domain columns automatically
- Normalize domains
- Remove duplicates
- Create scanning queues

Supported inputs:

```
example.com
www.example.com
https://example.com
http://example.com
```

The system will convert all inputs into a standardized format.

---

# 2. Website Scanner Module

## Included

The scanner will:

- Launch browser instances
- Visit websites automatically
- Render JavaScript content
- Monitor network requests
- Analyze website resources
- Collect detection signals

Technology:

- Playwright
- Chromium browser

---

# 3. Advertising Technology Detection Module

## Included Platforms

Version 1 supports detection of:

## Google

- Google Ads
- Google Conversion Tracking
- Google Tag Manager signals

## Meta

- Meta Pixel

## Microsoft

- Microsoft UET Tag

## TikTok

- TikTok Pixel

## LinkedIn

- LinkedIn Insight Tag

## Pinterest

- Pinterest Tag

---

# 4. Detection Intelligence Module

The system will not only show whether a technology exists.

It will also provide:

## Detection Confidence

Levels:

- High
- Medium
- Low
- None

---

## Detection Reason

Example:

```
Google Ads conversion tag detected
```

---

## Detection Method

Example:

```
Network Request
JavaScript
HTML Source
Cookie
```

---

## Prospect Score

Each website receives a score based on:

- Number of detected platforms
- Detection confidence
- Advertising signals

---

# 5. Database Module

## Included

SQLite database will store:

- Scan history
- Website results
- User settings
- Notes
- Tags
- Starred prospects
- Statistics

No external database server is required.

---

# 6. Dashboard Module

## Included

Dashboard will display:

- Total scans
- Total websites processed
- Ads detected count
- Average confidence
- Recent activity
- Previous scans

---

# 7. Prospect Management Module

## Included

Users can:

### Star Prospects

Save important websites.

---

### Add Notes

Example:

```
Need website redesign discussion
```

---

### Add Tags

Example:

```
Hot Lead
Follow Up
Contacted
```

---

### Search

Search by:

- Domain
- Notes
- Tags

---

# 8. Filtering Module

Users can filter results by:

- Advertising platform
- Confidence level
- Prospect score
- Scan status
- Starred status
- Tags

---

# 9. Export Module

Users can export:

## All Results

Complete scan database.

---

## Filtered Results

Only matching filtered websites.

Example:

```
Google Ads = YES
Confidence = HIGH
```

---

## Selected Results

Only manually selected websites.

---

## Starred Results

Only saved prospects.

---

## Failed Results

Only failed scans.

---

Supported formats:

- CSV
- Excel
- JSON

---

# 10. Error Handling Module

The system will handle:

- Website timeout
- SSL errors
- DNS errors
- Website unavailable
- Browser errors
- Blocked requests

---

# Version 1 Out of Scope

The following features are NOT included in Version 1.

---

## Cloud Platform

Not included:

- Online dashboard
- Cloud database
- Multi-user access

---

## User Authentication

Not included:

- Login system
- User accounts
- Permissions

---

## Subscription System

Not included:

- Payments
- Billing
- SaaS plans

---

## CRM Integration

Not included:

- HubSpot integration
- Salesforce integration
- Email automation

---

## AI Website Analysis

Not included in Version 1:

- Website redesign suggestions
- Copy analysis
- Conversion optimization recommendations

---

# Future Scope

Future versions may include:

## Version 2

- Better detection accuracy
- More advertising platforms
- Resume scanning
- Scheduled scans
- AI-based analysis

---

## Version 3

- Cloud synchronization
- Team workspace
- CRM integration
- Automated outreach
- AI sales assistant

---

# Technical Boundaries

The first version must remain:

- Local-first
- Simple to deploy
- Low cost
- Easy to maintain
- AI implementation friendly

---

# Scope Summary

Ads Detector Version 1 is a powerful local prospect intelligence application focused on:

```
CSV Upload

↓

Website Scanning

↓

Advertising Technology Detection

↓

Prospect Qualification

↓

Filtering

↓

Export
```

The goal is to build a reliable foundation that can later evolve into a complete marketing intelligence platform.
