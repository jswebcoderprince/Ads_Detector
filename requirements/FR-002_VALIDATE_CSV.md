# FR-002: CSV Validation

## Requirement ID

FR-002

---

## Requirement Name

CSV Data Validation and Cleaning

---

# Purpose

The CSV Validation module ensures that uploaded website data is clean, accurate, and ready for website scanning.

The system must analyze uploaded CSV files, identify invalid records, remove unnecessary data issues, and prepare a reliable scan queue.

---

# Related User Stories

- US-002: Validate Uploaded CSV
- US-003: Normalize Domains

---

# Functional Description

After a user uploads a CSV file, the system shall validate all website records before starting the scanning process.

The validation process includes:

1. Column analysis
2. Domain extraction
3. Domain normalization
4. Duplicate detection
5. Invalid domain removal
6. Validation summary generation
7. Scan queue creation

---

# Validation Workflow

```
Uploaded CSV

↓

Read File Structure

↓

Detect Domain Column

↓

Extract Domains

↓

Normalize Domains

↓

Remove Duplicates

↓

Check Validity

↓

Generate Validation Report

↓

Create Scan Queue
```

---

# 1. Column Detection

## Purpose

Identify which column contains website information.

---

## Supported Column Names

The system should recognize:

```
domain

website

url

website_url

site

web

homepage
```

---

## Column Detection Logic

Priority:

1. Exact domain match
2. URL-related column names
3. Column containing the highest number of valid domains

---

# 2. Domain Normalization

## Purpose

Convert different website formats into a standard format.

---

## Input Examples

```
https://www.example.com

http://example.com/page

www.example.com

example.com
```

---

## Output

```
example.com
```

---

## Normalization Rules

The system should remove:

- http://
- https://
- www.
- URL paths
- Query parameters
- Fragments
- Extra spaces

---

# 3. Duplicate Detection

## Purpose

Prevent scanning the same website multiple times.

---

## Example

Input:

```
example.com

www.example.com

https://example.com
```

After normalization:

```
example.com
```

Result:

```
1 unique domain
```

---

# 4. Invalid Domain Detection

The system should identify invalid records.

Examples:

Invalid:

```
hello

12345

abc@domain.com

empty value
```

Valid:

```
example.com

business.co.uk

company.org
```

---

# 5. Data Cleaning

The system should automatically remove:

- Empty rows
- Duplicate domains
- Invalid URLs
- Unsupported entries

---

# Validation Report

After processing, the system should show a summary.

Example:

```
CSV Validation Complete


Total Rows:

1000


Valid Domains:

930


Duplicates Removed:

50


Invalid Records:

20


Ready For Scan:

930
```

---

# User Actions After Validation

After reviewing the report, user can:

## Continue

Start website scanning.

---

## Cancel

Discard the uploaded data.

---

## Review Issues

View invalid records.

---

# Invalid Records View

The system should allow users to see:

| Domain | Reason |
|---|---|
| example | Invalid domain |
| empty | Missing value |
| abc@test.com | Email detected |

---

# Database Behavior

Before scanning:

Temporary validation data may be stored.

After user confirms:

A new scan session is created.

Stored information:

- Original file name
- Total records
- Valid records
- Removed records
- Creation date

---

# Performance Requirements

The validation process should:

- Handle 1000+ domains efficiently
- Avoid UI freezing
- Provide progress updates for large files

---

# Error Handling

## Missing Domain Data

Message:

```
No valid website domains were found.

Please upload a CSV containing website URLs.
```

---

## Unsupported Data Format

Message:

```
The CSV structure could not be recognized.
Please check your file format.
```

---

## Empty Dataset

Message:

```
No usable records are available for scanning.
```

---

# Acceptance Criteria

The feature is complete when:

## AC-001

System can analyze uploaded CSV files.

---

## AC-002

System detects domain columns automatically.

---

## AC-003

System removes duplicate websites.

---

## AC-004

System identifies invalid records.

---

## AC-005

System generates validation summary.

---

## AC-006

System creates a clean scan queue.

---

# Future Improvements

Possible enhancements:

- AI-powered column detection
- Automatic CSV correction
- Multiple file upload
- Google Sheets import
- Database import

---

# Summary

FR-002 ensures that Ads Detector never sends unreliable data into the scanning engine.

By cleaning and validating website lists before scanning, the system improves:

- Accuracy
- Performance
- Scan efficiency
- Result quality
