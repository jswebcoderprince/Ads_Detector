# PRODUCT_VISION.md

# Product Vision

## Vision Statement

Ads Detector exists to help agencies, marketers, and outbound sales
teams quickly identify websites that are likely investing in paid
advertising. Instead of manually inspecting hundreds of websites, users
should be able to upload a CSV and receive a reliable report within
minutes.

The application is intentionally focused on one problem: **detecting
advertising technologies on websites**.

------------------------------------------------------------------------

# Problem Statement

Manually checking websites for advertising technologies is slow,
repetitive, and inconsistent.

Common workflow today:

1.  Open website
2.  Open browser developer tools
3.  Search HTML
4.  Check network requests
5.  Repeat hundreds of times

This process does not scale.

Ads Detector automates this workflow using a real Chromium browser
driven by Playwright.

------------------------------------------------------------------------

# Product Objectives

## Primary Objectives

-   Upload CSV files containing domains.
-   Scan websites automatically.
-   Execute JavaScript before inspection.
-   Detect supported advertising technologies.
-   Export a clean CSV report.

## Secondary Objectives

-   Reduce manual research time.
-   Keep the interface extremely simple.
-   Make scans reliable even when some websites fail.

------------------------------------------------------------------------

# Target Audience

-   Web design agencies
-   Cold email agencies
-   PPC consultants
-   Lead generation specialists
-   Marketing researchers

------------------------------------------------------------------------

# Core Principles

1.  One purpose only.
2.  Local-first.
3.  Accuracy before speed.
4.  Real browser rendering.
5.  Modular architecture.
6.  Predictable behavior.
7.  Easy maintenance.

------------------------------------------------------------------------

# Version 1 Success Definition

Version 1 is successful if a user can:

-   Upload a CSV.
-   Scan 100+ websites.
-   Detect supported advertising technologies.
-   View progress in real time.
-   Export results without losing completed work.

------------------------------------------------------------------------

# What Version 1 Will NOT Do

The following are intentionally excluded:

-   SEO audits
-   Website speed testing
-   Contact extraction
-   AI recommendations
-   CRM integration
-   User accounts
-   Cloud synchronization
-   Databases

Keeping scope small improves reliability and reduces maintenance.

------------------------------------------------------------------------

# Guiding Design Philosophy

Every feature added to the application must answer one question:

> Does this improve advertising technology detection?

If the answer is "no", it does not belong in Version 1.

------------------------------------------------------------------------

# Long-Term Vision

Future versions may add optional modules, but the advertising detection
engine should remain the foundation of the application.

Potential future modules:

-   Additional advertising platforms
-   Scheduling recurring scans
-   Team workspaces
-   Historical scan comparison
-   API integrations

These ideas are outside the scope of Version 1.

------------------------------------------------------------------------

# Exit Criteria

This document is complete when all future implementation decisions can
be evaluated against the product vision above.
