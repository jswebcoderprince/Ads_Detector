# Confidence Scoring

## Overview

Confidence Scoring is the mechanism by which Ads Detector quantifies the certainty of each technology detection. Because detection is evidence-based and rule-driven, not every match carries equal certainty — some matches are backed by strong, unambiguous signals (e.g., a known vendor script URL), while others rely on weaker, more circumstantial signals (e.g., a generic cookie name pattern). Confidence Scoring translates the strength and quantity of matched evidence into a standardized, interpretable score attached to every detection result.

## Purpose

The purpose of this document is to:

- Define how confidence scores are calculated for each detected advertising, tracking, or analytics technology.
- Establish a consistent, deterministic scoring methodology used across all detection categories.
- Provide transparency into why a given technology was assigned a particular confidence level.
- Support the filtering system described in `FR-012_FILTERING_SYSTEM.md`, which allows users to filter results by confidence threshold.
- Ensure scoring behavior remains consistent with the evidence model defined in `DETECTION_ENGINE.md`.

## Detailed Explanation

### Scoring Model

Ads Detector uses a rule-based, additive confidence scoring model. Each detection rule that matches contributes a defined weight toward the overall confidence score for a given technology on a given domain. The final score is normalized to a fixed scale.

**Score Scale:**
- Confidence scores are expressed on a 0–100 numeric scale.
- Scores are additionally mapped to categorical labels for dashboard display.
  These bands are the canonical definition from `FR-008_CONFIDENCE_SCORING.md`,
  which is the single source of truth for confidence thresholds across the
  project:
  - **High Confidence:** 80–100
  - **Medium Confidence:** 50–79
  - **Low Confidence:** 20–49
  - **No Detection:** 0 (technology not present in results)

  Note: because every detected technology is assigned a score of at least 1
  (see Functional Requirements), scores of 1–19 fall below the Low band's
  lower bound but are still shown as Low — there is no "detected but None"
  state. A score of 0 is reserved exclusively for "not detected".

### Evidence Weighting

Each type of evidence carries a predefined weight based on its reliability:

| Evidence Type | Example | Typical Weight |
|---|---|---|
| Exact vendor script URL match | `googletagmanager.com/gtm.js` | High |
| Known tracking pixel request pattern | Facebook Pixel beacon URL | High |
| Cookie name signature | `_ga`, `_fbp` | Medium |
| Response header signature | Vendor-specific header | Medium |
| Generic pattern match | Partial URL substring match | Low |
| Behavioral inference | Timing/structure heuristics | Low |

### Score Aggregation

- When multiple pieces of evidence support the same technology, their weights are combined using a diminishing-returns aggregation function rather than simple summation, to prevent score inflation from redundant weak signals.
- A single strong, high-weight match (e.g., an exact vendor script match) can independently place a detection in the High Confidence range.
- Multiple low-weight matches alone cannot push a score into the High Confidence range without at least one medium- or high-weight corroborating signal.

### Determinism

- Given identical scan evidence, the confidence scoring algorithm must always produce the same score. No randomness or non-deterministic factors are introduced into the calculation.
- This determinism allows for reliable historical comparison across repeated scans of the same domain, supporting the scan history feature described in `FR-016_SCAN_HISTORY.md`.

## Functional Requirements

- Every detected technology must be assigned a confidence score between 1 and 100.
- Confidence scores must be recalculated on every scan; scores are not carried over from previous scans even for the same domain.
- The scoring engine must expose the individual evidence contributions that produced the final score, for use in the evidence display described in `DETECTION_ENGINE.md`.
- Confidence thresholds used for categorical labels (High/Medium/Low) must be configurable at the application level without requiring code changes.

## Technical Considerations

- The scoring engine operates as a distinct step in the detection pipeline, positioned after rule matching and before database storage, consistent with the workflow: Detection Engine → Confidence Scoring → Database Storage.
- Evidence weights must be stored in a centralized, versioned configuration rather than hard-coded across individual detection rules, to allow scoring calibration without modifying detection logic.
- Because scoring must remain deterministic and auditable, no machine-learning-based or probabilistic black-box scoring model is used in the current implementation; scoring is fully rule-based and explainable.

## Workflow / Process

```
Detection Engine Produces Matched Evidence
              ↓
Evidence Categorized by Type and Weight
              ↓
Diminishing-Returns Aggregation Applied
              ↓
Raw Score Normalized to 0–100 Scale
              ↓
Categorical Label Assigned (High / Medium / Low)
              ↓
Score and Evidence Breakdown Persisted to Database
```

## Error Handling

- If no evidence is matched for a given technology category, no score is generated and the technology is excluded from results for that domain, rather than defaulting to a zero-confidence entry.
- If the scoring configuration (evidence weights) is missing or malformed at runtime, the system must fail the scan with a clear configuration error rather than silently applying default weights that could produce misleading scores.
- Any scoring calculation exception must be logged with the domain, technology category, and raw evidence set to support debugging, in accordance with `ERROR_HANDLING.md`.

## Security Considerations

- Confidence scoring logic must not be exposed or modifiable through user-facing interfaces; only administrators with configuration access may adjust evidence weights.
- Scoring configuration files must be protected from unauthorized modification, since altered weights could be used to intentionally mask or falsely inflate detection results.

## Future Improvements

- Introduce per-technology-category calibration based on aggregated false-positive/false-negative feedback over time.
- Support confidence score decay or re-verification prompts for detections that rely on rapidly-changing vendor signatures.
- Provide a visual "evidence breakdown" panel in the dashboard showing exactly how each score was composed.
- Evaluate introducing a supervised scoring adjustment layer once sufficient labeled detection accuracy data is available, while preserving explainability.

## Summary

Confidence Scoring provides a consistent, deterministic, and explainable method for quantifying the certainty of every technology detection in Ads Detector. By combining weighted evidence through a diminishing-returns aggregation model and mapping results to both numeric and categorical scales, the system gives users clear, trustworthy signals about how strongly a given piece of evidence supports each detected advertising, tracking, or analytics technology.
