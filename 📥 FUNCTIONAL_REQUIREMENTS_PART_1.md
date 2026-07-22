# FUNCTIONAL REQUIREMENTS
# Part 1
## Document ID

ADS-FR-001

---

# Purpose

This document defines the functional requirements for Version 1 of the Ads Detector application.

Every requirement in this document is mandatory unless explicitly marked as optional.

---

# Requirement Priority Definitions

| Priority | Meaning |
|----------|----------|
| Critical | Required for Version 1 |
| High | Required before release |
| Medium | Nice to have |
| Low | Future improvement |

---

# FR-001
## Upload CSV

Priority

Critical

---

### Description

The application shall allow users to upload a CSV file from their local computer.

---

### Supported Formats

.csv only

---

### Maximum File Size

Default

100 MB

Configurable through application settings.

---

### User Flow

User clicks Upload CSV

↓

Operating system file picker opens

↓

User selects CSV

↓

Application validates file

↓

Application stores file temporarily

↓

Ready for scanning

---

### Validation Rules

The uploaded file must:

- Exist
- Have .csv extension
- Contain at least one row
- Be readable
- Use UTF-8 encoding whenever possible

---

### Invalid Cases

Reject if

- Empty file
- Unsupported extension
- Corrupted CSV
- Permission denied

---

### Error Messages

Empty CSV

```
The selected CSV contains no records.
```

Unsupported file

```
Only CSV files are supported.
```

Permission

```
Unable to read the selected file.
```

---

### Acceptance Criteria

✓ User selects CSV

✓ File uploads successfully

✓ Invalid files are rejected

✓ No application crash occurs

---

# FR-002
## Validate CSV

Priority

Critical

---

### Description

The application shall validate uploaded CSV files before scanning begins.

---

### Validation Rules

Check

- Empty rows
- Missing headers
- Invalid encoding
- Duplicate headers
- Invalid delimiters

---

### Allowed Delimiters

- Comma
- Semicolon

---

### Behaviour

If validation fails

Scanning must NOT begin.

---

### Acceptance Criteria

✓ Invalid CSV cannot start scanning.

✓ User receives meaningful error.

---

# FR-003
## Detect Domain Column

Priority

Critical

---

### Description

The application shall automatically identify which column contains website domains.

---

### Supported Header Names

Highest Priority

domain

website

url

site

homepage

---

### Detection Strategy

Step 1

Search for known header names.

Step 2

If multiple matches exist

Prefer

domain

↓

website

↓

url

---

### Content Detection

If headers are unknown

Inspect values.

Example

```
https://google.com
```

↓

Recognize as website column.

---

### Accepted Formats

google.com

www.google.com

https://google.com

http://google.com

---

### Invalid Values

test

hello

12345

example

---

### Acceptance Criteria

✓ Correct column selected automatically.

---

# FR-004
## Normalize Domains

Priority

Critical

---

### Description

Before scanning, every domain shall be normalized into a consistent format.

---

### Rules

Remove

http://

https://

www.

Trailing slash

Spaces

Convert

Google.COM

↓

google.com

---

### Examples

Input

```
HTTPS://WWW.Google.com/
```

Output

```
google.com
```

---

### Acceptance Criteria

Every website enters the scanner in normalized form.

---

# FR-005
## Create Scan Queue

Priority

Critical

---

### Description

The backend shall create a queue containing every normalized website.

---

### Queue Object

Each queue item shall contain

- Domain
- Status
- Retry Count
- Started Time
- Finished Time
- Result

---

### Initial Status

Pending

---

### Status Lifecycle

Pending

↓

Running

↓

Completed

or

↓

Failed

---

### Acceptance Criteria

Queue generated successfully.

---

# FR-006
## Launch Playwright Browser

Priority

Critical

---

### Description

The application shall launch a Chromium browser using Playwright.

---

### Requirements

Headless mode

Enabled

Browser reuse

Enabled

One browser instance

One browser context per website

---

### Browser Timeout

30 seconds

Configurable

---

### Browser Shutdown

Browser closes only after entire queue finishes.

---

### Acceptance Criteria

✓ Browser launches successfully.

✓ Browser reused efficiently.

✓ Memory leaks avoided.

---

# FR-007
## Scan Website

Priority

Critical

---

### Description

Each website shall be opened inside Playwright before advertisement detection begins.

---

### Scan Pipeline

Normalize URL

↓

Create Browser Context

↓

Open Website

↓

Wait for DOMContentLoaded

↓

Wait for Network Idle

↓

Capture

- HTML

- Scripts

- Network Requests

↓

Send to Detection Engine

↓

Store Result

↓

Close Context

---

### Timeout Behaviour

If timeout occurs

Retry once.

If second attempt fails

Mark Failed.

---

### Error Handling

Supported

- DNS Error
- SSL Error
- Timeout
- Connection Refused
- HTTP Errors

---

### Acceptance Criteria

✓ Website scanned.

✓ Errors logged.

✓ Failed website does not stop queue.

---

# Part 1 Complete

The next document continues with

FR-008

↓

FR-013

Advertisement Detection Engine.
