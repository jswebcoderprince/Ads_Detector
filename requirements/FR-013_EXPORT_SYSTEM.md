# FR-013: Export System

## Requirement ID

FR-013

---

## Requirement Name

Website Result Export Management System

---

# Purpose

The Export System allows users to export scanned website data into external files for further use.

The purpose of this module is to provide flexible exporting options while ensuring users can export only the required data instead of the complete scan dataset.

---

# Related User Stories

- US-016: Export Filtered Results
- US-017: Export Scan Results
- US-018: Export Starred Prospects

---

# Functional Description

The system shall allow users to export:

- Complete scan results
- Filtered results
- Selected websites
- Starred prospects
- Tagged websites

The export process must preserve data accuracy and structure.

---

# Export Workflow

```
Scan Results

↓

User Applies Filter

↓

Select Export Option

↓

Generate Export File

↓

Save File

↓

Download
```

---

# Supported Export Formats

Version 1 should support:

## CSV Export

Default format.

Example:

```
ads_detected_results.csv
```

---

## Excel Export

Optional support:

```
ads_detected_results.xlsx
```

---

## JSON Export

For future integrations.

Example:

```
scan_results.json
```

---

# Export Types

---

# 1. Full Scan Export

Exports all websites from a scan session.

Example:

```
Total Scanned:

1000 websites


Export:

1000 records
```

---

# 2. Filtered Export

Exports only filtered results.

Example:

Input:

```
1000 websites
```

Filter:

```
Ads Detected = YES
```

Result:

```
200 websites
```

Export:

```
200 records only
```

---

# 3. Selected Export

Users can manually select websites.

Example:

```
Selected:

50 websites
```

Export:

```
50 records
```

---

# 4. Starred Export

Exports only saved prospects.

Example:

```
Starred:

120 websites
```

Export:

```
120 records
```

---

# 5. Tagged Export

Exports websites based on tags.

Example:

Tag:

```
Hot Lead
```

Result:

```
80 websites
```

---

# Export Data Structure

Exported file should contain:

```
Domain

Original URL

Ads Detected

Detected Platforms

Confidence Score

Prospect Score

Classification

Tags

Notes

Scan Date
```

---

# Example CSV Output

```
domain,
ads_detected,
platforms,
confidence,
score,
category


example.com,
Yes,
Google Ads + Meta Pixel,
95,
92,
Hot Lead
```

---

# Filter Protection

Important rule:

Export must use current filtered results only.

Example:

Database:

```
1000 records
```

Active Filter:

```
Ads Detected = YES
```

Matching:

```
200 records
```

Export:

```
200 records
```

The remaining:

```
800 records
```

must not be included.

---

# Export Naming System

Generated files should have automatic names.

Example:

```
ads_detector_google_ads_results_20260722.csv
```

---

# Export History

The system should optionally store export activity.

Example:

```
Export Name

Date

Record Count

Export Type
```

---

# Database Requirements

Export history table:

```
exports
```

Fields:

```
id

export_name

export_type

record_count

file_format

created_at
```

---

# User Interface Requirements

Export button locations:

## Result Page

Options:

```
Export All

Export Filtered

Export Selected
```

---

## Starred Page

Option:

```
Export Starred
```

---

# Large Export Handling

The system should support:

```
10,000+ records
```

Requirements:

- Generate file in background
- Avoid UI freezing
- Show export progress

---

# Error Handling

## Export Failed

Message:

```
Unable to generate export file.
Please try again.
```

---

## No Data Available

Message:

```
No records available for export.
```

---

## File Permission Error

Message:

```
Unable to save file.
Please select another location.
```

---

# Security Requirements

Export files should:

- Contain only user-selected data
- Avoid exposing internal system information
- Remove unnecessary technical logs

---

# Acceptance Criteria

The feature is complete when:

## AC-001

Users can export scan results.

---

## AC-002

Filtered results export correctly.

---

## AC-003

Only selected records are included.

---

## AC-004

Starred prospects can be exported.

---

## AC-005

Export files contain required columns.

---

## AC-006

Original database remains unchanged.

---

# Future Improvements

Possible enhancements:

- Google Sheets export
- CRM integration
- Automatic email delivery
- Scheduled exports
- API-based export

---

# Summary

FR-013 provides a flexible export system that converts Ads Detector results into usable sales and marketing datasets.

The main goal is:

```
Scan 1000 Websites

↓

Filter 200 Ads Running Websites

↓

Export Only Those 200 Prospects
```

without mixing unwanted data.
