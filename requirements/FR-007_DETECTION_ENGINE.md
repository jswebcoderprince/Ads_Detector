# FR-007: Detection Engine

## Requirement ID

FR-007

---

## Requirement Name

Advertising Technology Detection Engine

---

# Purpose

The Detection Engine analyzes collected website signals and identifies advertising and marketing technologies installed on websites.

The engine converts raw scanner data into meaningful detection results.

---

# Related User Stories

- US-007: Detect Advertising Technologies
- US-008: Understand Detection Results
- US-009: View Prospect Score

---

# Functional Description

The Detection Engine receives collected website data from the Website Scanner and analyzes:

- HTML source
- JavaScript files
- Network requests
- Cookies
- Tracking identifiers

The engine then determines whether advertising technologies are present.

---

# Detection Workflow

```
Website Scanner Data

↓

Signal Processing

↓

Pattern Matching

↓

Technology Identification

↓

Confidence Calculation

↓

Generate Detection Result

↓

Store Result
```

---

# Supported Detection Platforms

Version 1 supports:

---

# 1. Google Advertising Technologies

The engine should detect:

## Google Ads

Possible signals:

```
googleadservices.com

doubleclick.net

conversion.js

AW-XXXXXXXX
```

---

## Google Tag Manager

Signals:

```
googletagmanager.com

GTM-XXXXXXX
```

---

## Google Analytics Marketing Signals

Signals:

```
google-analytics.com
gtag()
GA_MEASUREMENT_ID
```

---

# 2. Meta Advertising Technologies

The engine should detect:

## Meta Pixel

Signals:

```
connect.facebook.net

facebook pixel

fbq()

_fbp cookie
```

---

# 3. Microsoft Advertising

The engine should detect:

## Microsoft UET Tag

Signals:

```
bat.bing.com

uetq

Microsoft UET
```

---

# 4. TikTok Advertising

The engine should detect:

## TikTok Pixel

Signals:

```
analytics.tiktok.com

ttq

TikTok Pixel
```

---

# 5. LinkedIn Advertising

The engine should detect:

## LinkedIn Insight Tag

Signals:

```
snap.licdn.com

linkedin insight
```

---

# 6. Pinterest Advertising

The engine should detect:

## Pinterest Tag

Signals:

```
pintrk()

ct.pinterest.com
```

---

# Detection Methods

The engine should use multiple detection methods.

---

## 1. Script Detection

Analyze JavaScript resources.

Example:

Found:

```
connect.facebook.net/en_US/fbevents.js
```

Result:

```
Meta Pixel Detected
```

---

## 2. Network Detection

Analyze outgoing website requests.

Example:

Request:

```
googleadservices.com/pagead/conversion
```

Result:

```
Google Ads Detected
```

---

## 3. HTML Detection

Analyze page source.

Example:

Found:

```
gtag('config')
```

Result:

```
Google Tracking Detected
```

---

## 4. Cookie Detection

Analyze browser cookies.

Example:

Cookie:

```
_fbp
```

Result:

```
Meta Pixel Signal
```

---

# Detection Result Structure

Every detection should generate:

```
Technology

Status

Confidence

Detection Method

Reason

Evidence
```

---

# Example Result

```
Website:

example.com


Technology:

Google Ads


Status:

Detected


Confidence:

High


Method:

Network Request


Reason:

Google conversion endpoint found
```

---

# Confidence System

The engine should calculate confidence based on evidence strength.

---

## High Confidence

Conditions:

- Multiple signals found
- Known tracking script detected
- Valid tracking identifier found

Example:

```
Meta Pixel script

+

_fbp cookie
```

---

## Medium Confidence

Conditions:

- One strong signal found

Example:

```
Google Ads domain request
```

---

## Low Confidence

Conditions:

- Weak matching pattern

Example:

```
Generic marketing script
```

---

## None

No advertising signals found.

---

# Detection Rules Engine

Detection patterns should be stored separately.

Example:

```
detectors/

google_ads.py

meta_pixel.py

tiktok_pixel.py

linkedin.py
```

---

# Adding New Detectors

The architecture should allow adding new platforms without modifying existing code.

Example future additions:

- Snapchat Pixel
- Reddit Pixel
- Quora Pixel
- Amazon Ads

---

# False Positive Prevention

The engine should reduce incorrect detections.

Rules:

- Require multiple signals when possible
- Ignore unrelated scripts
- Validate known tracking patterns

---

# Database Storage

Detection results should be stored.

Recommended table:

```
detection_results
```

Fields:

```
id

scan_id

domain

technology

status

confidence

method

reason

evidence

created_at
```

---

# Error Handling

## Analysis Failed

Message:

```
Unable to analyze website signals.
```

---

## Unknown Signal

Message:

```
Unknown tracking pattern detected.
```

The system may store it for future analysis.

---

# Performance Requirements

The Detection Engine should:

- Analyze results quickly
- Support multiple websites
- Avoid repeated processing
- Cache known patterns

---

# Acceptance Criteria

The feature is complete when:

## AC-001

System detects supported advertising technologies.

---

## AC-002

System provides detection evidence.

---

## AC-003

System calculates confidence level.

---

## AC-004

System stores detection results.

---

## AC-005

New detectors can be added easily.

---

# Future Improvements

Possible enhancements:

- AI-based pattern detection
- Machine learning classification
- Automatic detector updates
- Community detection database

---

# Summary

FR-007 defines the intelligence core of Ads Detector.

The Detection Engine transforms technical website signals into actionable marketing information by identifying advertising platforms, calculating confidence, and generating qualified business insights.
