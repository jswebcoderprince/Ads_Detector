# Requirements Index

## Overview

This document provides a complete, quick-reference index of every functional requirement (FR) document contained in the `requirements/` directory, ordered by requirement number and grouped by the workflow stage each requirement belongs to.

## Purpose

The purpose of this document is to:

- Give contributors a single, scannable list of every functional requirement without needing to open each file individually.
- Map each requirement to the core workflow stage it supports.
- Serve as the definitive checklist against which `docs/ACCEPTANCE_CRITERIA.md` and `docs/TESTING.md` coverage can be verified.

## Detailed Explanation

### Full Requirement List

| ID | Title | Workflow Stage |
|---|---|---|
| FR-001 | Upload CSV | CSV Upload |
| FR-002 | Validate CSV | CSV Validation |
| FR-003 | Detect Domain Column | CSV Validation |
| FR-004 | Create Scan Session | Domain Processing / Scan Queue |
| FR-005 | Scan Queue Management | Scan Queue |
| FR-006 | Website Scanner | Website Scanner |
| FR-007 | Detection Engine | Detection Engine |
| FR-008 | Confidence Scoring | Confidence Scoring |
| FR-009 | Database Management | Database Storage |
| FR-010 | Dashboard | Dashboard |
| FR-011 | Result Management | Dashboard |
| FR-012 | Filtering System | Filtering |
| FR-013 | Export System | Export Results |
| FR-014 | Star and Bookmark System | Star / Notes / Tags |
| FR-015 | Notes and Tag Management | Star / Notes / Tags |
| FR-016 | Scan History | Database Storage / Dashboard |
| FR-017 | Application Settings | Cross-Cutting |
| FR-018 | Notification System | Cross-Cutting |
| FR-019 | Security and Privacy | Cross-Cutting |
| FR-020 | Download Results | Export Results |

### Grouping by Core Workflow

```
CSV Upload            → FR-001
CSV Validation         → FR-002, FR-003
Domain Processing      → FR-004
Scan Queue             → FR-004, FR-005
Website Scanner        → FR-006
Detection Engine       → FR-007
Confidence Scoring     → FR-008
Database Storage       → FR-009, FR-016
Dashboard              → FR-010, FR-011, FR-016
Filtering              → FR-012
Star / Notes / Tags    → FR-014, FR-015
Export Results         → FR-013, FR-020
Cross-Cutting          → FR-017, FR-018, FR-019
```

## Functional Requirements

- This index must list every FR document present in the `requirements/` directory; no FR file may exist without a corresponding entry here.
- The workflow stage mapping must be updated whenever a requirement's scope changes such that it affects a different stage than originally documented.

## Technical Considerations

- Some requirements span more than one workflow stage (e.g., `FR-004` touches both Domain Processing and Scan Queue, `FR-016` touches both Database Storage and Dashboard); this index lists the primary stage(s) for navigational purposes, not an exhaustive dependency map.
- Cross-cutting requirements (`FR-017` through `FR-019`) apply across multiple or all workflow stages rather than a single point in the pipeline.

## Workflow / Process

```
New FR Document Added to requirements/
              ↓
Entry Added to This Index Table
              ↓
Workflow Stage Mapping Assigned
              ↓
Cross-Checked Against requirements/README.md Numbering Overview
```

## Error Handling

- Discrepancies between this index and the actual contents of `requirements/` must be corrected immediately upon discovery, treated as a documentation defect.

## Security Considerations

- Not directly applicable; `FR-019_SECURITY_AND_PRIVACY.md` remains the authoritative source for security-specific requirement detail.

## Future Improvements

- Add direct hyperlinks to each FR file once the documentation is published in a environment that supports relative linking (e.g., a rendered GitHub Pages site).
- Introduce a status column (Draft, Approved, Implemented, Deprecated) once requirement lifecycle tracking is formalized.

## Summary

This index provides a complete, workflow-organized reference to all twenty functional requirements governing Ads Detector, from CSV upload through result download, supporting fast navigation and ensuring full coverage traceability across the requirements set.
