# Diagrams Directory

## Overview

This directory contains all Mermaid (`.mmd`) diagram source files used to visually represent Ads Detector's architecture, data model, and processing flows. These diagrams complement the written documentation in `docs/` by providing a visual reference for the same systems described in text.

## Purpose

The purpose of this directory is to:

- Provide version-controlled, text-based diagram sources that can be rendered by any Mermaid-compatible tool or embedded directly into Markdown documentation.
- Keep architectural and workflow diagrams synchronized with the written documentation as the system evolves.
- Give new contributors a fast visual orientation to the system before reading detailed engineering documents.

## Detailed Explanation

### Files in This Directory

- `SYSTEM_ARCHITECTURE.mmd` — a diagram of the overall modular architecture, corresponding to `docs/SYSTEM_ARCHITECTURE.md`.
- `APPLICATION_FLOW.mmd` — a diagram of the end-to-end user and data flow, from CSV upload through export, corresponding to `docs/FUNCTIONAL_OVERVIEW.md`.
- `COMPONENT_DIAGRAM.mmd` — a diagram showing the relationships and boundaries between core modules (CSV Processor, Scanner Engine, Detection Engine, Database Layer, Export System, User Interface).
- `DATABASE_RELATIONSHIP.mmd` — an entity-relationship diagram of the database schema, corresponding to `docs/DATABASE_DESIGN.md`.
- `DETECTION_PIPELINE.mmd` — a diagram of the detection and confidence scoring pipeline, corresponding to `docs/DETECTION_ENGINE.md` and `docs/CONFIDENCE_SCORING.md`.

### Rendering Diagrams

Each `.mmd` file can be rendered using any Mermaid-compatible renderer, including:

- The Mermaid CLI (`mmdc`)
- Mermaid Live Editor (browser-based)
- GitHub's native Mermaid rendering when embedded in a Markdown code block with the `mermaid` language tag

## Functional Requirements

- Every diagram file must remain valid, parseable Mermaid syntax.
- Diagrams must be updated whenever the corresponding architecture, workflow, or schema changes in a way that affects the visual representation.
- New diagrams added to this directory must be referenced from this README.

## Technical Considerations

- Diagrams are the single visual source of truth for their respective subject; if a diagram and its corresponding written documentation disagree, both must be reconciled as part of the same change.
- Diagram files should remain focused — one diagram per concern — rather than combining unrelated systems into a single, overly complex diagram.

## Workflow / Process

```
Architecture or Workflow Changes
              ↓
Corresponding .mmd File Updated
              ↓
Diagram Re-Rendered and Visually Verified
              ↓
Corresponding docs/ File Updated to Match
              ↓
Both Changes Reviewed Together in the Same Pull Request
```

## Error Handling

- Invalid Mermaid syntax that fails to render must be corrected before merge; a broken diagram file should never be committed to the main branch.

## Security Considerations

- Diagrams must not include actual credentials, internal hostnames, or sensitive configuration values, even as illustrative placeholder text.

## Future Improvements

- Add automated CI validation that renders every `.mmd` file to catch syntax errors before merge.
- Add a sequence diagram illustrating a single end-to-end scan request, including error and timeout paths.
- Add a deployment/network diagram once containerized deployment topology is finalized in `docs/DEPLOYMENT.md`.

## Summary

The `diagrams/` directory provides text-based, version-controlled Mermaid diagrams that visually represent Ads Detector's architecture, workflow, and data model, keeping visual documentation synchronized with the platform's written specifications.
