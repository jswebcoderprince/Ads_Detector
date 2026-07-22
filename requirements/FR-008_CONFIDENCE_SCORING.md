# FR-008: Confidence Scoring System

## Requirement ID

FR-008

---

## Requirement Name

Detection Confidence and Quality Scoring

---

# Purpose

The Confidence Scoring module evaluates the reliability of detected advertising technologies and assigns a confidence level to each result.

The purpose is to help users understand how trustworthy each detection result is and prioritize valuable prospects.

---

# Related User Stories

- US-008: Understand Detection Results
- US-009: View Prospect Score
- US-011: Filter Results

---

# Functional Description

After the Detection Engine identifies advertising signals, the Confidence Scoring system analyzes the collected evidence and generates:

- Confidence Level
- Confidence Score
- Detection Quality
- Prospect Priority

---

# Scoring Workflow

```
Detection Result

↓

Analyze Evidence

↓

Calculate Confidence Score

↓

Assign Confidence Level

↓

Generate Prospect Quality

↓

Store Result
```

---

# Confidence Score

Each detection result receives a score between:

```
0 - 100
```

Higher score means stronger evidence.

---

# Confidence Levels

The system uses four confidence categories:

```
High

Medium

Low

None
```

---

# High Confidence

Score:

```
80 - 100
```

Conditions:

- Multiple strong signals detected
- Official tracking script found
- Valid tracking ID identified

Example:

```
Meta Pixel:

fbq() found

+

connect.facebook.net script found

+

_fbp cookie found


Confidence:

95/100

Level:

High
```

---

# Medium Confidence

Score:

```
50 - 79
```

Conditions:

- One strong signal detected
- Limited supporting evidence

Example:

```
Google Ads request detected


Confidence:

65/100

Level:

Medium
```

---

# Low Confidence

Score:

```
20 - 49
```

Conditions:

- Weak signal detected
- Pattern partially matched

Example:

```
Possible marketing script found


Confidence:

35/100

Level:

Low
```

---

# No Detection

Score:

```
0
```

Conditions:

- No advertising signals found

Result:

```
Not Detected
```

---

# Evidence Weight System

Each detection signal receives a weight.

Example:

| Signal | Weight |
|---|---:|
| Official tracking script | 40 |
| Valid tracking ID | 30 |
| Network endpoint | 20 |
| Cookie signal | 10 |

---

# Example Calculation

Website:

```
example.com
```

Detected:

```
Google Ads Script

+

Conversion ID

+

Network Request
```

Calculation:

```
Script:

40 points


Conversion ID:

30 points


Network:

20 points


Total:

90/100
```

Result:

```
High Confidence
```

---

# Multiple Platform Scoring

If multiple advertising platforms are detected:

Additional value should be considered.

Example:

```
Google Ads

+

Meta Pixel

+

LinkedIn Insight
```

Indicates stronger marketing activity.

---

# Prospect Score

The system should generate an overall website prospect score.

Range:

```
0 - 100
```

---

# Prospect Score Factors

The score should consider:

## Advertising Activity

Weight:

```
40%
```

More platforms increase score.

---

## Detection Confidence

Weight:

```
30%
```

Higher confidence increases score.

---

## Marketing Signals

Weight:

```
20%
```

Examples:

- Multiple tracking systems
- Conversion tracking
- Analytics tools

---

## Website Quality Signals

Weight:

```
10%
```

Future:

- SSL
- Mobile support
- Website technology

---

# Example Prospect Score

```
Website:

business.com


Detected:

Google Ads

Meta Pixel


Confidence:

High


Prospect Score:

92/100
```

---

# Result Classification

The system should classify prospects.

---

## Hot Prospect

Score:

```
80 - 100
```

Example:

```
Multiple ads platforms detected
High confidence
```

---

## Warm Prospect

Score:

```
50 - 79
```

Example:

```
Some marketing activity detected
```

---

## Cold Prospect

Score:

```
0 - 49
```

Example:

```
No strong advertising signals
```

---

# Database Storage

The system should store:

Table:

```
confidence_scores
```

Fields:

```
id

domain

technology

confidence_score

confidence_level

prospect_score

classification

created_at
```

---

# User Interface Requirements

Results should display:

Example:

```
Domain:

example.com


Ads:

Google Ads

Meta Pixel


Confidence:

High (92%)


Prospect:

Hot Lead
```

---

# Filtering Support

Users should be able to filter by:

- Confidence level
- Score range
- Prospect category

Examples:

```
Show only:

High Confidence


Show only:

Score > 80
```

---

# Error Handling

## Missing Evidence

Message:

```
Unable to calculate confidence score.
Insufficient detection data.
```

---

## Invalid Score

The system should prevent:

```
Score < 0

Score > 100
```

---

# Acceptance Criteria

The feature is complete when:

## AC-001

Every detection result receives a confidence score.

---

## AC-002

System assigns correct confidence levels.

---

## AC-003

System generates prospect scores.

---

## AC-004

Users can filter results using scores.

---

## AC-005

Scores are stored permanently.

---

# Future Improvements

Possible enhancements:

- Machine learning scoring model
- Industry-based scoring
- Revenue prediction
- AI lead qualification
- Competitor analysis

---

# Summary

FR-008 creates a quality measurement system for Ads Detector.

Instead of only showing whether ads exist, the application can determine:

- How reliable the detection is
- How valuable the website may be
- Which prospects should be prioritized first
