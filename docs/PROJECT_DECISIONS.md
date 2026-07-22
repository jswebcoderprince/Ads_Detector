# Project Decisions

## Project Name

Ads Detector

---

# 1. Overview

This document records the important technical and product decisions made during the development of Ads Detector.

The purpose is to maintain consistency and explain why specific technologies, architectures, and approaches were selected.

---

# 2. Application Type Decision

## Decision

Ads Detector will be designed as a modular application that can support both desktop and web deployment.

---

## Reason

A modular structure provides:

- Easier development
- Better maintenance
- Future scalability
- Ability to convert into SaaS later

---

# 3. Database Decision

## Decision

SQLite is selected as the initial database.

---

## Reason

SQLite provides:

- Simple setup
- No external database server required
- Easy backup
- Good performance for local applications

---

## Future Plan

The system can migrate to:

- PostgreSQL
- MySQL
- Cloud databases

when scaling requirements increase.

---

# 4. Architecture Decision

## Decision

The application will follow a modular architecture.

---

## Modules

```
CSV Processing Engine

Scanner Engine

Detection Engine

Database Layer

Export System

User Interface
```

---

## Reason

Separating modules provides:

- Easier debugging
- Independent improvements
- Cleaner code structure

---

# 5. Scanner Technology Decision

## Decision

Browser automation will be used for website analysis.

Recommended:

```
Playwright
```

---

## Reason

Browser-based scanning allows detection of:

- Dynamic JavaScript
- Tracking scripts
- Network requests
- Cookies

---

# 6. Detection Approach Decision

## Decision

Detection will use rule-based analysis combined with evidence collection.

---

## Reason

Rule-based detection provides:

- Explainable results
- Easy updates
- Better accuracy control

---

Example:

```
Found:

facebook.com/tr request

+

fbq() script


Result:

Meta Pixel Detected
```

---

# 7. CSV Processing Decision

## Decision

CSV files will be processed before scanning.

---

## Reason

Pre-processing improves:

- Scan efficiency
- Data quality
- Duplicate handling

---

Processing:

```
Upload

↓

Validation

↓

Cleaning

↓

Queue Creation
```

---

# 8. Queue Processing Decision

## Decision

Website scanning will use a queue system.

---

## Reason

Large datasets require:

- Controlled processing
- Retry support
- Better resource management

---

# 9. Evidence-Based Detection Decision

## Decision

Every detection result must contain evidence.

---

## Reason

Users need to understand why a technology was detected.

---

Example:

```
Technology:

Google Ads


Evidence:

googleadservices.com detected
```

---

# 10. Security Decision

## Decision

All external website data will be treated as untrusted.

---

Security measures:

- Input validation
- File validation
- Browser isolation
- Safe data handling

---

# 11. Export System Decision

## Decision

Users can export filtered results only.

---

## Reason

Users should be able to:

- Select important leads
- Avoid exporting unnecessary data
- Manage large datasets efficiently

---

# 12. Future Scalability Decision

The system should be designed to support:

- Multiple users
- Cloud deployment
- API access
- AI-based analysis

---

# 13. Final Decision Summary

The project prioritizes:

```
Simple Architecture

Reliable Detection

Clean Data Processing

Future Scalability

Maintainable Code
```

All future development should follow these decisions.
