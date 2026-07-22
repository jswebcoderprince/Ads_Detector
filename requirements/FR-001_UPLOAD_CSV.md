# FR-001: CSV Upload

## Requirement ID

FR-001

---

## Requirement Name

CSV File Upload

---

# Purpose

The CSV Upload module allows users to import a list of website domains into Ads Detector for automated scanning.

The system must provide a simple way to upload website data and prepare it for validation and scanning.

---

# Related User Stories

- US-001: Upload Website List
- US-002: Validate Uploaded CSV
- US-003: Normalize Domains

---

# Functional Description

The system shall allow users to upload CSV files containing website domain information.

After upload, the system will:

1. Receive the CSV file.
2. Verify file compatibility.
3. Read CSV structure.
4. Detect available columns.
5. Identify possible domain columns.
6. Prepare data for validation.

---

# Supported File Format

The first version supports:

```
.csv
```

Future support may include:

```
.xlsx
.txt
```

---

# User Flow

```
User Opens Application

↓

Navigate to Upload Section

↓

Select CSV File

↓

System Reads File

↓

Validate File Format

↓

Detect Domain Column

↓

Show Upload Summary

↓

Continue to Validation
```

---

# Upload Interface Requirements

The upload interface should provide:

## File Selection

User can:

- Click upload button
- Select CSV file
- Drag and drop CSV file

---

## Upload Information

After selecting a file, the system should display:

- File name
- File size
- Total rows
- Detected columns

Example:

```
File:

business_domains.csv


Rows:

1000


Detected Column:

domain
```

---

# CSV Structure Requirements

The system should support different column names.

Examples:

Accepted:

```
domain

website

url

website_url

site
```

The system should automatically identify the most likely domain column.

---

# Domain Data Processing

The system should accept:

Examples:

```
example.com

www.example.com

https://example.com

http://example.com/page
```

The system should prepare them for normalization.

---

# Validation Rules

Before continuing, the system must check:

## File Validation

- File extension must be CSV.
- File should not be empty.
- File size should be within allowed limits.

---

## Data Validation

The system should check:

- Empty rows
- Missing domains
- Invalid URLs
- Duplicate domains

---

# Upload Limits

Version 1 target:

```
Minimum:

1,000 domains


Future:

10,000+ domains
```

The system should handle large files without freezing the interface.

---

# Error Handling

## Invalid File Type

Example:

```
Error:

Unsupported file format.

Please upload a CSV file.
```

---

## Empty File

Example:

```
Error:

The uploaded CSV does not contain any data.
```

---

## No Domain Column Found

Example:

```
Error:

Unable to find website domain information.

Please upload a CSV containing website URLs.
```

---

## Corrupted CSV

Example:

```
Error:

The CSV file could not be processed.
Please upload a valid file.
```

---

# Database Behavior

At upload stage:

The system should NOT permanently save data yet.

Temporary data should be stored until validation is completed.

After successful validation:

A new scan session will be created.

---

# Security Requirements

The system should:

- Validate uploaded files
- Prevent unsupported file execution
- Limit excessive file sizes
- Handle malformed CSV safely

---

# Acceptance Criteria

The feature is considered complete when:

## AC-001

User can upload a valid CSV file.

---

## AC-002

System detects domain-related columns automatically.

---

## AC-003

System displays upload summary.

---

## AC-004

Invalid files show meaningful error messages.

---

## AC-005

Uploaded data is prepared for validation.

---

# Future Improvements

Possible future enhancements:

- Excel upload support
- Automatic column mapping
- Saved CSV templates
- Cloud import
- Google Sheets integration

---

# Summary

FR-001 defines the first step of the Ads Detector workflow.

The CSV Upload module acts as the entry point where raw website data enters the system and prepares it for validation, scanning, and prospect intelligence processing.
