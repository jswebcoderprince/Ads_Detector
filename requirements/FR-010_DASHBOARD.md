# FR-010: Dashboard

## Requirement ID

FR-010

---

## Requirement Name

Application Dashboard and Statistics View

---

# Purpose

The Dashboard module provides users with a central overview of Ads Detector activity.

The dashboard allows users to quickly understand:

- Current scan status
- Previous scan performance
- Detection statistics
- Prospect opportunities

---

# Related User Stories

- US-005: Monitor Scan Progress
- US-021: View Statistics
- US-019: View Scan History

---

# Functional Description

When the application starts, the system shall display a dashboard containing important application information.

The dashboard should provide a quick summary without requiring users to open individual modules.

---

# Dashboard Workflow

```
Application Opens

↓

Load Database

↓

Retrieve Statistics

↓

Calculate Metrics

↓

Display Dashboard
```

---

# Dashboard Layout

The dashboard should contain:

```
------------------------------------------------

Total Websites Scanned

Total Ads Detected

Hot Prospects

Active Scan Status


------------------------------------------------

Recent Scans


------------------------------------------------

Detection Statistics


------------------------------------------------

Quick Actions

------------------------------------------------
```

---

# 1. Summary Cards

The dashboard should display key metrics.

---

## Total Websites Scanned

Shows:

```
Number of websites processed
```

Example:

```
12,540 Websites
```

---

## Ads Detected

Shows:

```
Total websites with advertising signals
```

Example:

```
4,820 Detected
```

---

## Hot Prospects

Shows:

```
High-value websites
```

Example:

```
350 Hot Leads
```

---

## Active Scan

Shows current scanning status.

Example:

```
Scanning:

450 / 1000
```

---

# 2. Scan Progress Section

During an active scan, dashboard should display:

```
Current Scan:

US Roofing Leads


Progress:

45%


Completed:

450


Failed:

12


Remaining:

538
```

---

# 3. Recent Scan History

The dashboard should show recent scans.

Information:

```
Scan Name

Date

Total Websites

Status

Results
```

Example:

```
Roofing Campaign

22 July 2026

1000 Websites

Completed

230 Ads Found
```

---

# 4. Detection Statistics

The dashboard should display advertising technology statistics.

Example:

```
Google Ads

450 Websites


Meta Pixel

320 Websites


TikTok Pixel

85 Websites
```

---

# 5. Confidence Overview

The dashboard should display result quality.

Example:

```
High Confidence:

700


Medium:

350


Low:

100
```

---

# 6. Prospect Classification

Display lead categories:

```
Hot Leads

Warm Leads

Cold Leads
```

Example:

```
Hot:

250


Warm:

500


Cold:

300
```

---

# 7. Quick Actions

Dashboard should provide shortcuts.

Actions:

## Upload CSV

Navigate to CSV upload page.

---

## Start New Scan

Create new scan session.

---

## View Results

Open result management.

---

## Export Data

Open export module.

---

# 8. Search Access

Dashboard should provide quick search.

Search by:

- Domain
- Scan ID
- Prospect name
- Tag

---

# 9. Refresh Behavior

The dashboard should update automatically.

During active scans:

Refresh:

```
Every few seconds
```

or

```
Real-time update
```

---

# Database Data Sources

Dashboard information should be generated from:

```
scan_sessions

websites

detection_results

confidence_scores

tags
```

---

# Performance Requirements

Dashboard should:

- Load quickly
- Handle thousands of records
- Avoid unnecessary database queries
- Use optimized calculations

---

# Error Handling

## Database Unavailable

Message:

```
Unable to load dashboard data.
Please restart the application.
```

---

## No Data Available

Message:

```
No scan history available.

Upload a CSV file to start scanning.
```

---

# User Interface Requirements

The dashboard should be:

- Clean
- Simple
- Easy to understand
- Suitable for non-technical users

---

# Acceptance Criteria

The feature is complete when:

## AC-001

Dashboard loads when application starts.

---

## AC-002

Summary statistics are displayed.

---

## AC-003

Active scan progress is visible.

---

## AC-004

Recent scan history is available.

---

## AC-005

Users can access important actions quickly.

---

## AC-006

Dashboard updates after new scans.

---

# Future Improvements

Possible enhancements:

- Charts and graphs
- AI recommendations
- Industry analytics
- Lead conversion tracking
- Team dashboards

---

# Summary

FR-010 defines the main user interface of Ads Detector.

The dashboard transforms raw scan information into a clear business overview, allowing users to quickly understand their scanning activity and prospect opportunities.
