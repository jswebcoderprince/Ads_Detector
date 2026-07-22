# Database Design

## Project Name

Ads Detector

---

# 1. Overview

This document defines the database architecture of Ads Detector.

The database is responsible for storing:

- User scan data
- Website information
- Detection results
- Prospect management data
- Application settings
- System history

---

# 2. Database Technology

Version 1 Database:

```
SQLite
```

Database File:

```
ads_detector.db
```

---

# 3. Database Goals

The database should provide:

## Reliability

Data should remain available after application restart.

---

## Performance

Support thousands of websites and scan records.

---

## Simplicity

Easy local deployment and maintenance.

---

## Scalability

Structure should support future migration to PostgreSQL or cloud databases.

---

# 4. Database Architecture

```
Application

      |

      |

Database Layer

      |

      |

SQLite Database

      |

      |

Tables
```

---

# 5. Main Database Entities

The database contains:

```
scan_sessions

websites

scan_results

detections

notes

tags

website_tags

exports

notifications

settings
```

---

# 6. Database Relationship Diagram

```
scan_sessions

        |

        |

    websites

        |

        |

   scan_results

        |

        |

   detections


websites

   |

   |

notes


websites

   |

   |

website_tags

   |

   |

tags
```

---

# 7. Table Structures

---

# Table: scan_sessions

Purpose:

Stores every scanning operation.

---

Columns:

| Column | Type | Description |
|-|-|-|
| id | INTEGER | Primary key |
| scan_name | TEXT | Scan title |
| total_domains | INTEGER | Total websites |
| completed_domains | INTEGER | Completed count |
| failed_domains | INTEGER | Failed count |
| status | TEXT | Scan status |
| created_at | DATETIME | Creation time |
| completed_at | DATETIME | Completion time |

---

Example:

```
USA Roofing Campaign

1000 Domains

Status:

Completed
```

---

# Table: websites

Purpose:

Stores website/domain information.

---

Columns:

| Column | Type | Description |
|-|-|-|
| id | INTEGER | Primary key |
| domain | TEXT | Website domain |
| url | TEXT | Full URL |
| created_at | DATETIME | Added date |

---

Example:

```
example.com

https://example.com
```

---

# Table: scan_queue

Purpose:

Controls scanning tasks.

---

Columns:

| Column | Type |
|-|-|
| id | INTEGER |
| scan_id | INTEGER |
| website_id | INTEGER |
| status | TEXT |
| started_at | DATETIME |
| completed_at | DATETIME |

---

Status:

```
pending

processing

completed

failed
```

---

# Table: scan_results

Purpose:

Stores final website scan output.

---

Columns:

| Column | Type |
|-|-|
| id | INTEGER |
| website_id | INTEGER |
| scan_id | INTEGER |
| ads_detected | BOOLEAN |
| confidence_score | INTEGER |
| prospect_score | INTEGER |
| created_at | DATETIME |

---

# Table: detections

Purpose:

Stores detected advertising technologies.

---

Columns:

| Column | Type |
|-|-|
| id | INTEGER |
| website_id | INTEGER |
| platform | TEXT |
| evidence | TEXT |
| detected_at | DATETIME |

---

Example:

```
Google Ads

Meta Pixel

TikTok Pixel
```

---

# Table: notes

Purpose:

Stores user notes.

---

Columns:

| Column | Type |
|-|-|
| id | INTEGER |
| website_id | INTEGER |
| note_text | TEXT |
| created_at | DATETIME |
| updated_at | DATETIME |

---

# Table: tags

Purpose:

Stores custom tags.

---

Columns:

| Column | Type |
|-|-|
| id | INTEGER |
| tag_name | TEXT |
| created_at | DATETIME |

---

Example:

```
Hot Lead

USA

Follow Up
```

---

# Table: website_tags

Purpose:

Many-to-many relationship between websites and tags.

---

Columns:

| Column | Type |
|-|-|
| id | INTEGER |
| website_id | INTEGER |
| tag_id | INTEGER |

---

Example:

```
example.com

Tags:

Hot Lead

USA
```

---

# Table: exports

Purpose:

Stores export history.

---

Columns:

| Column | Type |
|-|-|
| id | INTEGER |
| file_name | TEXT |
| export_type | TEXT |
| record_count | INTEGER |
| created_at | DATETIME |

---

Example:

```
roofing_leads.csv

200 records
```

---

# Table: notifications

Purpose:

Stores application notifications.

---

Columns:

| Column | Type |
|-|-|
| id | INTEGER |
| title | TEXT |
| message | TEXT |
| type | TEXT |
| is_read | BOOLEAN |
| created_at | DATETIME |

---

# Table: settings

Purpose:

Stores application configuration.

---

Columns:

| Column | Type |
|-|-|
| id | INTEGER |
| setting_name | TEXT |
| setting_value | TEXT |
| updated_at | DATETIME |

---

Example:

```
timeout = 30

concurrency = 5
```

---

# 8. Database Indexing

For performance, indexes should be created on:

```
websites.domain

scan_results.score

scan_results.ads_detected

detections.platform

tags.tag_name
```

---

# 9. Data Integrity Rules

The database should enforce:

- Unique domains
- Valid relationships
- Required fields
- Foreign keys

---

# 10. Foreign Key Relationships

Example:

```
scan_sessions

        |

        |

scan_queue.scan_id


websites

        |

        |

scan_results.website_id


websites

        |

        |

notes.website_id
```

---

# 11. Backup Strategy

Database backup file:

```
ads_detector_backup.db
```

Backup should include:

- Scan history
- Results
- Notes
- Tags
- Settings

---

# 12. Migration Support

Future database migration:

```
SQLite

↓

PostgreSQL

↓

Cloud Database
```

---

# 13. Security Rules

Database should:

- Remain local
- Prevent unauthorized access
- Validate queries
- Protect user data

---

# 14. Performance Requirements

Database should support:

```
100,000+ websites

Millions of detection records
```

Requirements:

- Proper indexing
- Pagination
- Optimized queries

---

# 15. Summary

The Ads Detector database provides a structured storage system for the entire application.

Data flow:

```
CSV Upload

↓

Scan Session

↓

Website Records

↓

Detection Results

↓

Prospect Management

↓

Export
```

The database design allows Ads Detector to scale from a local tool into a complete website intelligence platform.
