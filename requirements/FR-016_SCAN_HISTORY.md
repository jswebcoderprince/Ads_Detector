# FR-016: Scan History Management

## Requirement ID

FR-016

---

## Requirement Name

Previous Scan History and Archive Management

---

# Purpose

The Scan History module stores and manages previous scanning operations.

The purpose of this module is to allow users to access, review, organize, and manage previous scan sessions without losing historical data.

---

# Related User Stories

- US-019: View Scan History
- US-020: Reopen Previous Scan
- US-021: Manage Old Results

---

# Functional Description

The system shall automatically save every completed or interrupted scan session into scan history.

Users should be able to:

- View previous scans
- Open old results
- Search scan sessions
- Delete unwanted scans
- Export previous results

---

# Scan History Workflow

```
New Scan Created

↓

Scanning Process

↓

Results Generated

↓

Save Scan History

↓

Available For Future Access
```

---

# Scan History List

The application should provide a dedicated page:

```
Scan History
```

---

# History Table

Each scan record should display:

| Field | Description |
|-|-|
| Scan Name | User or system name |
| Scan ID | Unique identifier |
| Date | Creation date |
| Total Websites | Number scanned |
| Ads Found | Detected websites |
| Status | Completed/Failed |
| Actions | Manage scan |

---

# Example

```
Campaign:

USA Roofing Leads


Date:

22 July 2026


Websites:

1000


Ads Detected:

240


Status:

Completed
```

---

# Opening Previous Scan

Users should be able to click:

```
View Results
```

and access old scan data.

---

# Previous Scan Details

The system should display:

```
Scan Information

↓

Website Results

↓

Detection Data

↓

Scores

↓

Tags

↓

Notes
```

---

# Search Scan History

Users should be able to search by:

- Scan name
- Scan ID
- Date
- Number of websites

---

# Filter Scan History

Available filters:

```
Completed Scans

Failed Scans

Recent Scans

Large Scans
```

---

# Reopen Scan

Users should be able to reopen previous scans.

Example:

```
July Roofing Campaign

↓

Open

↓

View 1000 Results
```

---

# Delete Scan

Users should be able to remove unwanted scan sessions.

Before deletion:

Confirmation:

```
Are you sure you want to delete this scan?

All related results will be removed.
```

---

# Delete Rules

Deleting a scan should remove:

```
Scan Session

Queue Data

Detection Results

Scores
```

Optional:

Keep:

```
Export History
```

---

# Archive Support

Future-ready support for archiving old scans.

Example:

```
Active Scans

↓

Archived Scans
```

---

# Scan Comparison

Future support:

Compare two scans.

Example:

```
July Campaign

VS

August Campaign
```

Comparison:

- New detected websites
- Removed websites
- Score changes
- Platform changes

---

# Database Requirements

Main table:

```
scan_sessions
```

Required fields:

```
id

scan_id

session_name

total_domains

completed_domains

failed_domains

status

created_at

completed_at
```

---

# History Relationship

Structure:

```
scan_sessions

        |

        |

scan_queue

        |

        |

websites

        |

        |

results
```

---

# Data Retention

The system should not automatically delete scan history.

User controls:

- Keep forever
- Delete manually
- Archive

---

# Performance Requirements

The system should support:

```
1000+ scan sessions
```

Requirements:

- Pagination
- Indexed search
- Optimized loading

---

# User Interface Requirements

The Scan History page should provide:

```
+ New Scan

+ Search

+ Filter

+ Open

+ Export

+ Delete
```

---

# Error Handling

## History Load Failed

Message:

```
Unable to load scan history.
```

---

## Scan Not Found

Message:

```
The selected scan does not exist.
```

---

## Delete Failed

Message:

```
Unable to delete scan.
Please try again.
```

---

# Acceptance Criteria

The feature is complete when:

## AC-001

Completed scans are automatically saved.

---

## AC-002

Users can view previous scans.

---

## AC-003

Users can reopen old results.

---

## AC-004

Users can delete unwanted scans.

---

## AC-005

Historical data remains available after restart.

---

## AC-006

Previous results can be exported again.

---

# Future Improvements

Possible enhancements:

- Cloud backup
- Scan scheduling
- Automatic campaign reports
- Scan comparison analytics
- Team sharing

---

# Summary

FR-016 provides long-term data management for Ads Detector.

Instead of losing previous scans, users can maintain a complete history of:

```
Campaign

↓

Scan

↓

Detected Ads

↓

Qualified Prospects
```

This allows Ads Detector to become a reusable lead intelligence platform rather than a one-time scanner.
