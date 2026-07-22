# Export Engine

## Overview

The Export Engine is the module responsible for generating downloadable output files from the currently filtered set of scan results within Ads Detector. It sits at the final stage of the core workflow, converting in-application data — detected technologies, confidence scores, tags, notes, and star status — into a portable file format that users can share, archive, or analyze outside the application.

## Purpose

The purpose of this document is to:

- Define the responsibilities and boundaries of the Export Engine within the modular architecture.
- Describe how the Export Engine interacts with the Filtering System to ensure only relevant results are exported.
- Specify the structure and integrity guarantees of exported files.
- Provide a reference for extending export format support in the future.

## Detailed Explanation

### Core Responsibility

The Export Engine's defining responsibility is to export **only the currently filtered result set**, never the entire database, unless the user has explicitly cleared all filters. This directly supports the core feature requirement that users can narrow down to relevant websites and export precisely that subset.

### Export Trigger

- The Export Engine is invoked when a user initiates an export action from the Dashboard.
- At invocation time, the Export Engine receives the active filter state (technology filters, confidence thresholds, tag filters, star status) from the Filtering System, not the raw unfiltered dataset.

### Export Format

- The default export format is CSV, chosen for compatibility with spreadsheet tools and downstream data pipelines commonly used by Ads Detector's target users (agencies and marketers evaluating home service business websites).
- Each exported row corresponds to one scanned domain and includes:
  - Domain name
  - Detected technologies (advertising, tracking, analytics) with their individual confidence scores
  - Overall confidence classification (High/Medium/Low)
  - Star status
  - Notes
  - Tags
  - Scan date and scan status

### Export Generation Process

1. The Export Engine receives the active filter criteria from the Filtering System.
2. It queries the Database Layer for all records matching the current filter criteria.
3. It transforms the queried records into the export schema, flattening nested detection and evidence data into exportable columns.
4. It writes the transformed data to a temporary output file in the configured export directory.
5. It returns a download reference to the User Interface, which presents the file to the user.

### Column Consistency

- Exported files must maintain a consistent column schema across exports, even when some domains have no detected technologies, empty notes, or no tags, to ensure the output can be reliably consumed by external spreadsheet tools or scripts.

## Functional Requirements

- The Export Engine must only include domains that match all currently active filters at the moment the export is triggered.
- Exported files must be valid, well-formed CSV files that open correctly in standard spreadsheet applications.
- The Export Engine must support exporting zero, one, or many rows without error, including the edge case where a filter combination matches no domains.
- Export operations must not modify or lock the underlying scan data during generation.

## Technical Considerations

- The Export Engine is a downstream consumer of the Database Layer and Filtering System; it must not duplicate filtering logic but instead delegate filter evaluation to the Filtering System's existing query criteria to avoid inconsistent results between what the Dashboard displays and what gets exported.
- Because export files may be requested for large filtered result sets, the Export Engine should stream rows to the output file rather than loading the entire result set into memory at once.
- The export schema must remain versioned so that historical exports can be understood even if the underlying data model evolves over time.

## Workflow / Process

```
User Applies Filters on Dashboard
              ↓
User Triggers Export Action
              ↓
Export Engine Receives Active Filter Criteria
              ↓
Database Layer Queried for Matching Records Only
              ↓
Records Transformed into Export Schema
              ↓
Output File Generated (CSV)
              ↓
Download Reference Returned to User Interface
              ↓
User Downloads Filtered Export File
```

## Error Handling

- If the Database Layer query fails during export generation, the Export Engine must return a clear error to the user rather than producing a partial or corrupted file.
- If the filtered result set is empty, the Export Engine must generate a valid CSV file containing only the header row, along with a clear message to the user indicating that no matching records were found.
- Temporary export files that fail to generate completely must be discarded rather than left in a partially written state accessible for download.
- Export generation timeouts (e.g., for unusually large result sets) must be handled gracefully with a descriptive message rather than a silent failure.

## Security Considerations

- Exported files must not include internal database identifiers, raw error traces, or any data not intended for end-user consumption.
- Notes and tag fields included in exports must be sanitized to prevent CSV injection attacks (e.g., formula injection via leading `=`, `+`, `-`, or `@` characters when opened in spreadsheet applications).
- Temporary export files must be stored in a location not directly accessible via a public URL, and must be cleaned up after a reasonable retention window to avoid unauthorized access to previously generated exports.

## Future Improvements

- Add support for additional export formats (e.g., JSON, Excel `.xlsx`) alongside the default CSV format.
- Introduce scheduled or automated recurring exports for users who need periodic snapshots of filtered results.
- Support customizable column selection, allowing users to choose which fields are included in a given export.
- Add export history tracking so users can review and re-download previously generated exports without re-running filters.

## Summary

The Export Engine converts the currently filtered set of scan results into a portable, well-structured CSV file, ensuring users receive precisely the data they have narrowed down to — never the full dataset unless explicitly requested. By delegating filter evaluation to the Filtering System and streaming data through the Database Layer, the Export Engine maintains consistency, performance, and security while supporting the platform's core export use case.
