# Glossary

## Overview

This document provides a centralized glossary of terms, acronyms, and domain-specific vocabulary used throughout the Ads Detector documentation, codebase, and product interface. It ensures that all contributors, reviewers, and users share a consistent understanding of terminology.

## Purpose

The purpose of this document is to:

- Prevent ambiguity or misinterpretation of key terms across documentation files.
- Provide a fast reference for new contributors unfamiliar with the platform's domain-specific language.
- Ensure that terminology used in `PRODUCT_VISION.md`, `SYSTEM_ARCHITECTURE.md`, `DETECTION_ENGINE.md`, and related documents remains consistent.
- Reduce onboarding friction for developers, QA engineers, and stakeholders joining the project.

## Detailed Explanation

### Core Terms

**Ads Detector**
The website intelligence platform described throughout this documentation, which analyzes websites and detects advertising, tracking, analytics, and marketing technologies.

**Domain**
A website address (e.g., `example.com`) submitted for scanning, in its normalized, canonical form.

**Domain Normalization**
The process of converting raw domain input (which may include protocols, trailing slashes, or mixed casing) into a canonical lowercase, protocol-stripped format.

**CSV Processor**
The module responsible for accepting, validating, cleaning, and normalizing uploaded CSV files containing domain lists.

**Scan Queue**
The ordered collection of validated, unique domains awaiting processing by the Website Scanner.

**Scan Session**
A logical grouping of domains submitted together for scanning, typically corresponding to a single CSV upload.

**Website Scanner**
The module that uses Playwright-based browser automation to visit a domain, render its content, and capture network requests, headers, cookies, and DOM data required for detection.

**Detection Engine**
The rule-based module that analyzes captured scan data to identify advertising, tracking, and analytics technologies present on a scanned website.

**Evidence**
The specific data point (e.g., a matched script URL, cookie name, or response header) that justifies a given technology detection.

**Confidence Score**
A numeric value (0–100) and corresponding categorical label (High/Medium/Low) representing the certainty of a given technology detection, as defined in `CONFIDENCE_SCORING.md`.

**Detection Category**
A classification of the type of technology being detected, such as Advertising, Tracking Pixel, or Analytics.

**Dashboard**
The primary user interface view where scanned domains, their detected technologies, and confidence scores are displayed.

**Filtering System**
The feature that allows users to narrow down displayed and exportable results based on technology, confidence score, tags, and star status.

**Star / Starred Domain**
A user-applied marker indicating that a particular domain is important or noteworthy, used for quick identification and filtering.

**Tag**
A user-defined label applied to a domain to support categorization and filtering, with support for multiple tags per domain.

**Note**
A free-text annotation a user attaches to a domain, independent of scan results.

**Export**
The action of generating a downloadable file (typically CSV) containing the currently filtered set of scan results.

**Scan History**
The record of all previous scans performed on a given domain, preserved across re-scans.

**Rule-Based Detection**
The detection methodology used by Ads Detector, in which technologies are identified through predefined pattern-matching rules rather than probabilistic or machine-learning inference.

**Modular Architecture**
The system design approach used by Ads Detector, in which functionality is separated into independent modules: CSV Processor, Scanner Engine, Detection Engine, Database Layer, Export System, and User Interface.

### Acronyms

| Acronym | Meaning |
|---|---|
| FR | Functional Requirement |
| AC | Acceptance Criteria |
| CSV | Comma-Separated Values |
| DOM | Document Object Model |
| SQL | Structured Query Language |
| API | Application Programming Interface |
| UI | User Interface |
| CI | Continuous Integration |
| ADR | Architecture Decision Record |

## Functional Requirements

- Every new domain-specific term introduced in future documentation must be added to this glossary at the time it is introduced.
- Terminology used in the User Interface (labels, tooltips, messages) must match the definitions in this glossary exactly, to avoid confusing end users with inconsistent wording.

## Technical Considerations

- This glossary is a living document; its accuracy depends on being updated alongside changes to `SYSTEM_ARCHITECTURE.md`, `DETECTION_ENGINE.md`, and functional requirement documents.
- Terms defined here should be treated as canonical — if a conflicting definition appears elsewhere in the documentation, this glossary takes precedence and the conflicting document should be corrected.

## Workflow / Process

```
New Term Introduced in Code, Docs, or UI
              ↓
Contributor Checks Glossary for Existing Definition
              ↓
If Missing: Term Added to Glossary in Same Pull Request
              ↓
Glossary Reviewed Alongside Documentation Changes
              ↓
Glossary Merged as Part of Documentation Update
```

## Error Handling

- Not applicable in the traditional runtime sense; however, inconsistent terminology discovered during documentation review should be treated as a documentation defect and corrected promptly.

## Security Considerations

- Not applicable directly, though consistent terminology around security-sensitive terms (e.g., "evidence," "confidence score," "detection") helps avoid miscommunication during security reviews and audits.

## Future Improvements

- Add cross-references linking each glossary term to the specific documentation files where it is used in depth.
- Introduce a searchable, generated glossary page if the documentation is ever published as a static site.
- Expand the glossary to include common third-party advertising and analytics vendor terminology (e.g., specific tracking technology names) as detection coverage grows.

## Summary

This glossary provides a single, authoritative source of terminology for Ads Detector, covering core architectural concepts, workflow stages, and domain-specific vocabulary. Maintaining this document ensures that all contributors and stakeholders communicate using a shared, unambiguous vocabulary as the platform and its documentation continue to evolve.
