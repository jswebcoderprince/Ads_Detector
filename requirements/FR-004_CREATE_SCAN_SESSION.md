# FR-004: Create Scan Session

## Requirement ID

FR-004

---

## Requirement Name

Scan Session Creation and Management

---

# Purpose

The Scan Session module creates and manages individual website scanning tasks.

Each scanning operation must have its own unique session so that the system can track:

- Uploaded data
- Scan progress
- Results
- Errors
- Completion status
- History

---

# Related User Stories

- US-004: Start Website Scan
- US-005: Monitor Scan Progress
- US-019: View Scan History

---

# Functional Description

When a user starts a scan, the system shall create a new scan session.

A scan session represents one complete scanning operation from start to finish.

---

# Scan Session Workflow

```
User Clicks Start Scan

↓

Check Validated Domains

↓

Create Scan Session

↓

Generate Scan ID

↓

Store Session Information

↓

Create Website Queue

↓

Start Scanner Engine
```

---

# Scan Session Information

Each scan session should contain:

| Field | Description |
|---|---|
| Scan ID | Unique identifier |
| Session Name | User-defined or automatic name |
| Created Date | Scan creation time |
| Total Domains | Number of websites |
| Status | Current scan state |
| Progress | Completion percentage |
| Start Time | Scan start timestamp |
| End Time | Completion timestamp |

---

# Scan ID Generation

Every scan must receive a unique identifier.

Example:

```
SCAN-20260722-001
```

Format:

```
SCAN + DATE + NUMBER
```

---

# Session Status

The system should support:

```
Created

Queued

Running

Paused

Completed

Failed

Cancelled
```

---

# Session Creation Rules

Before creating a scan session:

The system must verify:

- CSV validation completed
- Valid domains exist
- User confirmed scanning

---

# Empty Scan Prevention

If no valid domains exist:

The system should prevent scan creation.

Message:

```
No valid websites are available for scanning.
Please upload a valid CSV file.
```

---

# Scan Queue Creation

After session creation:

The system should create individual scan tasks.

Example:

```
Scan Session

SCAN-001


Queue:


1. example.com

2. business.com

3. company.org
```

---

# Queue Data Structure

Each queued website should contain:

```
Queue ID

Scan ID

Domain

Status

Created Time

Priority
```

---

# Database Storage

When a scan session is created, the following information should be stored.

## Scan Session Table

Example:

```
scan_sessions
```

Fields:

```
id

scan_id

name

total_domains

completed_domains

failed_domains

status

created_at

started_at

completed_at
```

---

# User Interface Behavior

After clicking:

```
Start Scan
```

The application should:

1. Disable duplicate scan start.
2. Show scan initialization.
3. Display generated scan ID.
4. Navigate to scan progress screen.

---

# Multiple Scan Support

Version 1 should support viewing previous scans.

Example:

```
Today's Scan

SCAN-001


Yesterday

SCAN-002
```

---

# Scan Naming

Default:

```
Scan - 22 July 2026
```

Future:

Allow users to customize names.

Example:

```
US Roofing Prospects July
```

---

# Error Handling

## No Valid Data

```
Unable to create scan.

No valid domains found.
```

---

## Database Error

```
Scan session could not be created.

Please try again.
```

---

## Duplicate Start

```
A scan is already running.
```

---

# Acceptance Criteria

The feature is complete when:

## AC-001

System creates a unique scan session.

---

## AC-002

Each scan has a unique Scan ID.

---

## AC-003

System stores scan information in SQLite.

---

## AC-004

System generates website scan queue.

---

## AC-005

User can view scan status.

---

## AC-006

Previous scan sessions remain available.

---

# Future Improvements

Possible enhancements:

- Pause and resume sessions
- Scheduled scans
- Cloud sync
- Shared scan history
- Scan templates

---

# Summary

FR-004 establishes the foundation for managing scanning operations.

By creating independent scan sessions, Ads Detector can:

- Track progress
- Store history
- Recover from failures
- Support future scalability

Each website scan operation becomes a structured and manageable process.
