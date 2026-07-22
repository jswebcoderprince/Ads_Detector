# Ads Detector PRD

## Version

-   Version: 1.0
-   Status: Draft
-   Target: Local Web Application

# 1. Product Overview

## Purpose

Ads Detector is a local web application that accepts a CSV containing
website domains and determines whether each website shows evidence of
running paid advertising technologies.

The application focuses only on ad detection. No SEO auditing,
performance analysis, contact extraction, CRM, or AI features are
included.

## Primary Goal

Allow an agency owner to upload a CSV of hundreds or thousands of
domains and receive a downloadable report indicating which domains
appear to use advertising technologies.

------------------------------------------------------------------------

# 2. Project Scope

## Included

-   CSV Upload
-   Automatic Domain Detection
-   Playwright-based Website Scanning
-   JavaScript Rendering
-   Google Ads Detection
-   Meta Pixel Detection
-   Google Remarketing Detection
-   Microsoft UET Detection
-   TikTok Pixel Detection
-   LinkedIn Insight Detection
-   Pinterest Tag Detection
-   Progress Tracking
-   CSV Export

## Excluded

-   SEO
-   PageSpeed
-   AI
-   Lead Scoring
-   Contact Extraction
-   Authentication
-   Database

------------------------------------------------------------------------

# 3. Technology Stack

Frontend: - React - Vite - TailwindCSS

Backend: - FastAPI - Python 3.12+

Scanner: - Playwright Chromium

Utilities: - Pandas - Requests - BeautifulSoup (fallback parsing)

------------------------------------------------------------------------

# 4. User Flow

1.  User opens the local application.
2.  User uploads a CSV.
3.  System detects the domain column automatically.
4.  User clicks Start Scan.
5.  Backend scans every website.
6.  Progress updates in real time.
7.  User downloads the final CSV report.

------------------------------------------------------------------------

# 5. Detection Rules

Google Ads: - AW- - googleadservices.com - google_conversion_id -
gtag(...AW-...)

Meta: - fbq( - fbevents.js - connect.facebook.net

Google Remarketing: - googleads.g.doubleclick.net

TikTok: - ttq.track - analytics.tiktok.com

LinkedIn: - snap.licdn.com

Microsoft: - bat.bing.com

Pinterest: - pintrk

Result Logic:

If ANY supported advertising technology is detected:

Result = Running Ads

Otherwise:

Result = No Evidence

------------------------------------------------------------------------

# 6. CSV Input

Supported headers:

-   domain
-   website
-   url

If multiple columns exist, the application should automatically identify
the website/domain column.

------------------------------------------------------------------------

# 7. Output Columns

-   Domain
-   Status
-   Google Ads
-   Meta Pixel
-   Google Remarketing
-   TikTok Pixel
-   LinkedIn Insight
-   Microsoft UET
-   Pinterest
-   Result
-   Scan Time

------------------------------------------------------------------------

# 8. Performance Requirements

-   Parallel scanning
-   Configurable concurrency
-   Browser reuse
-   Retry failed websites once
-   Timeout per website: configurable

------------------------------------------------------------------------

# 9. Error Handling

Handle:

-   DNS failure
-   SSL failure
-   Timeout
-   Redirect loops
-   Connection refused

Errors should never stop the entire scan.

------------------------------------------------------------------------

# 10. API

POST /upload

POST /scan

GET /progress

GET /results

GET /download

------------------------------------------------------------------------

# 11. UI

Single dashboard containing:

-   Upload CSV
-   Start Scan
-   Progress Bar
-   Results Table
-   Download CSV

------------------------------------------------------------------------

# 12. Acceptance Criteria

-   Upload CSV successfully.
-   Detect supported advertising technologies.
-   Show scan progress.
-   Export CSV.
-   Continue scanning even if some websites fail.

------------------------------------------------------------------------

# 13. Future Versions

Reserved for future expansion. Not part of Version 1.
