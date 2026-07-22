# UI/UX Specification

## Overview

This document defines the user interface and user experience specification for Ads Detector, covering the Dashboard, Filtering System, Star/Notes/Tags interactions, CSV upload flow, and Export experience. It describes the expected layout, interaction patterns, and usability principles that guide the User Interface module's implementation.

## Purpose

The purpose of this document is to:

- Define a consistent, predictable user experience across all core features of the platform.
- Ensure the interface supports the platform's primary users — agencies and marketers evaluating home service business websites — efficiently.
- Provide a reference for frontend implementation that aligns with the underlying data model and workflow described in `SYSTEM_ARCHITECTURE.md` and `FUNCTIONAL_OVERVIEW.md`.
- Establish usability principles that apply consistently as new features are added.

## Detailed Explanation

### Primary Screens

**1. CSV Upload Screen**
- A clear drag-and-drop or file-picker upload area accepting `.csv` files.
- Immediate feedback on file acceptance, including a validation summary (valid rows, invalid rows, duplicates) once processing completes.
- A visible option to review and download a report of excluded/invalid rows.

**2. Scan Progress View**
- A real-time or near-real-time indicator of scan queue progress, showing counts of pending, in-progress, completed, and failed scans.
- Ability to navigate away from this view without interrupting the underlying scan process.

**3. Dashboard**
- A tabular or card-based view listing all scanned domains, with columns/fields for: domain name, detected technologies (summarized), overall confidence classification, star status, tags, and scan date.
- Pagination or virtualized scrolling for large result sets, consistent with performance expectations in `PERFORMANCE.md`.
- Each domain row/card supports drill-down into a detailed view showing full detection evidence per technology.

**4. Detailed Domain View**
- Displays all detected technologies for a domain, grouped by category (Advertising, Tracking Pixel, Analytics).
- For each detected technology, displays the confidence score and the underlying evidence (matched script, cookie, or header) that justified the detection.
- Provides inline controls for starring the domain, adding/editing notes, and adding/removing tags.

**5. Filtering Panel**
- Accessible filter controls for technology type, confidence score threshold, tags, and star status.
- Filters combine using clear, visible logic (e.g., "all conditions must match") consistent with `FR-012_FILTERING_SYSTEM.md`.
- A visible "reset filters" action to quickly return to the full unfiltered result set.

**6. Export Flow**
- An export action available directly from the filtered Dashboard view, clearly indicating that only the current filtered set will be exported.
- A confirmation state showing the number of rows to be exported before the file is generated.
- A clear success state with a download link once the export completes.

### Interaction Principles

- **Immediate feedback.** Every user action (filtering, starring, tagging, exporting) should produce visible, immediate feedback, even if the underlying operation is asynchronous.
- **Non-destructive actions.** Filtering, starring, and tagging must never alter or delete underlying scan data; these are purely presentational and metadata operations.
- **Progressive disclosure.** Summary information is shown at the Dashboard level; detailed evidence is only shown when a user explicitly drills into a domain, to avoid overwhelming the primary view.
- **Consistency.** Iconography, terminology, and interaction patterns (e.g., how filters are applied, how tags are added) must remain consistent across all screens, using the terms defined in `GLOSSARY.md`.

## Functional Requirements

- The interface must clearly distinguish between scan status states (pending, in progress, completed, failed, blocked, timeout).
- The interface must never allow a user to trigger an export without a visible indication of how many rows will be included.
- Star, note, and tag interactions must persist immediately upon user action, with visible confirmation, and must not be lost if the user navigates away before a full page reload.
- The interface must display validation and error messages in clear, non-technical language for user-facing issues (e.g., "3 rows were skipped because they were not valid domains") while preserving technical detail in logs per `LOGGING.md`.

## Technical Considerations

- The User Interface consumes data through the internal API layer described in `API_SPECIFICATION.md`; UI components should not assume direct access to the Database Layer.
- Real-time or near-real-time scan progress updates require either polling or a push-based mechanism (e.g., WebSockets or server-sent events); the chosen mechanism must be resilient to temporary disconnects without losing progress state.
- Filtering and pagination logic on the frontend must remain in sync with the Filtering System's backend query logic to avoid discrepancies between what is displayed and what would be exported.

## Workflow / Process

```
User Uploads CSV
        ↓
Upload Screen Shows Validation Summary
        ↓
Scan Progress View Displays Real-Time Queue Status
        ↓
Dashboard Populates as Scans Complete
        ↓
User Applies Filters
        ↓
User Reviews Detailed Evidence per Domain (Optional)
        ↓
User Stars / Tags / Notes Domains of Interest
        ↓
User Triggers Export of Filtered Results
        ↓
Export Confirmation and Download Provided
```

## Error Handling

- Upload errors (invalid file type, oversized file) must be displayed immediately and clearly, without requiring the user to inspect logs or technical output.
- Scan failures (timeouts, blocked sites) must be visually distinguished from successful scans on the Dashboard, rather than presented as if no data exists.
- If the Filtering System returns zero results for a given filter combination, the interface must display a clear "no matching results" state rather than an empty, ambiguous table.
- Export failures must present a clear retry option rather than leaving the user uncertain whether the export succeeded.

## Security Considerations

- User-entered notes and tags must be rendered with proper output encoding in the interface to prevent stored cross-site scripting.
- The interface must not expose internal database identifiers, raw error stack traces, or internal configuration values in any user-facing screen.
- File upload components must enforce client-side file type and size restrictions as a first line of defense, in addition to authoritative server-side validation.

## Future Improvements

- Introduce customizable Dashboard column configuration, allowing users to choose which fields are visible.
- Add bulk actions (e.g., bulk tagging, bulk starring) for users working with large filtered result sets.
- Introduce saved filter presets so users can quickly reapply frequently used filter combinations.
- Explore a comparison view allowing users to compare detection results for the same domain across multiple scan history entries.

## Summary

The UI/UX Specification defines the core screens, interaction patterns, and usability principles for Ads Detector's User Interface module. By emphasizing immediate feedback, non-destructive metadata operations, progressive disclosure of detection evidence, and consistent terminology, the interface aims to give users — particularly agencies and marketers evaluating home service business websites — an efficient, trustworthy experience across the full workflow from CSV upload through filtered export.
