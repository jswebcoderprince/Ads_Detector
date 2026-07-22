# FR-009: Database Management

## Requirement ID

FR-009

---

## Requirement Name

Local SQLite Database Management System

---

# Purpose

The Database Management module is responsible for storing, organizing, and retrieving all application data locally.

The system will use SQLite as the default database engine to provide:

- Fast local storage
- Easy deployment
- No external database dependency
- User data ownership

---

# Related User Stories

- US-019: View Scan History
- US-020: Save Application Settings
- US-012: Star Important Prospects
- US-013: Add Notes
- US-014: Add Tags

---

# Functional Description

The application shall maintain a local SQLite database containing:

- Scan sessions
- Website records
- Queue information
- Detection results
- Confidence scores
- User organization data
- Application settings

---

# Database Architecture

The database structure:

```
SQLite Database

│
├── scan_sessions
│
├── scan_queue
│
├── websites
│
├── detection_results
│
├── confidence_scores
│
├── tags
│
├── website_tags
│
├── notes
│
├── settings
│
└── exports
```

---

# Database Location

Default:

```
local application storage
```

Example:

```
ads_detector.db
```

---

# Table Definitions

---

# 1. scan_sessions Table

## Purpose

Stores every scanning operation.

---

Fields:

```
id

scan_id

session_name

total_domains

completed_domains

failed_domains

status

created_at

started_at

completed_at
```

---

Example:

```
SCAN-20260722-001

1000 domains

Status:

Completed
```

---

# 2. websites Table

## Purpose

Stores website information.

---

Fields:

```
id

domain

root_domain

original_url

created_at
```

---

Example:

```
Domain:

example.com


Root:

example.com
```

---

# 3. scan_queue Table

## Purpose

Controls website scanning tasks.

---

Fields:

```
id

scan_id

website_id

status

retry_count

priority

started_at

completed_at
```

---

Possible status:

```
Pending

Processing

Completed

Failed

Cancelled
```

---

# 4. detection_results Table

## Purpose

Stores detected advertising technologies.

---

Fields:

```
id

website_id

technology

status

method

reason

evidence

created_at
```

---

Example:

```
Technology:

Google Ads


Status:

Detected


Method:

Network Request
```

---

# 5. confidence_scores Table

## Purpose

Stores detection reliability scores.

---

Fields:

```
id

website_id

confidence_score

confidence_level

prospect_score

classification

created_at
```

---

Example:

```
Confidence:

92


Level:

High


Classification:

Hot Lead
```

---

# 6. notes Table

## Purpose

Stores user notes for prospects.

---

Fields:

```
id

website_id

note_text

created_at

updated_at
```

---

Example:

```
Needs website redesign discussion
```

---

# 7. tags Table

## Purpose

Stores user-created labels.

---

Fields:

```
id

tag_name

created_at
```

---

Example:

```
Hot Lead

Follow Up

Contacted
```

---

# 8. website_tags Table

## Purpose

Creates relationship between websites and tags.

---

Fields:

```
id

website_id

tag_id
```

---

Example:

```
example.com

↓

Hot Lead
```

---

# 9. settings Table

## Purpose

Stores application configuration.

---

Fields:

```
id

setting_name

setting_value

updated_at
```

---

Examples:

```
scan_timeout = 30

concurrency = 5
```

---

# 10. exports Table

## Purpose

Tracks exported files.

---

Fields:

```
id

export_type

file_name

record_count

created_at
```

---

Example:

```
Export:

Filtered Results


Records:

200
```

---

# Database Relationships

Relationship structure:

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

detection_results

        |

        |

confidence_scores
```

---

# Data Integrity Rules

The system must ensure:

- No duplicate domains
- Valid foreign relationships
- No orphan records
- Accurate scan history

---

# Database Operations

The application must support:

## Create

Examples:

- New scan session
- New website
- New detection result

---

## Read

Examples:

- Load history
- View results
- Search prospects

---

## Update

Examples:

- Change notes
- Update scan status
- Modify tags

---

## Delete

Examples:

- Remove scan history
- Delete unwanted prospects

---

# Backup Requirements

The system should allow database backup.

Backup file:

```
ads_detector_backup.db
```

Backup should include:

- All scans
- Results
- Notes
- Tags
- Settings

---

# Database Performance

Requirements:

- Use indexing for domain search
- Optimize large result queries
- Support 10,000+ records

---

# Security Requirements

Database should:

- Remain local
- Not expose user data
- Protect stored prospect information

---

# Migration Support

Future versions should support database migrations.

Example:

```
Version 1 Database

↓

Version 2 Database Upgrade
```

---

# Error Handling

## Database Connection Failed

Message:

```
Unable to open database.

Please restart the application.
```

---

## Corrupted Database

Message:

```
Database integrity issue detected.

Please restore from backup.
```

---

# Acceptance Criteria

The feature is complete when:

## AC-001

SQLite database is created automatically.

---

## AC-002

All required tables exist.

---

## AC-003

Scan data is stored correctly.

---

## AC-004

Detection results are linked to websites.

---

## AC-005

Notes, tags, and stars work correctly.

---

## AC-006

Database backup can be created.

---

# Future Improvements

Possible enhancements:

- PostgreSQL support
- Cloud database sync
- Database encryption
- Multi-user database
- Advanced analytics storage

---

# Summary

FR-009 defines the data foundation of Ads Detector.

A properly structured SQLite database allows the application to:

- Save scan history
- Manage prospects
- Store intelligence results
- Support future expansion

The database layer acts as the permanent memory of the application.
