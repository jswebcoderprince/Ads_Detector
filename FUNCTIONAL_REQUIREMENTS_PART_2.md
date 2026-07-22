# FUNCTIONAL_REQUIREMENTS_PART_2.md

# Advertisement Detection Requirements (FR-008 → FR-013)

## Purpose
This document defines the functional requirements for the advertisement detection engine.

## FR-008 Detect Google Ads
Priority: Critical

### Detection Sources
- Rendered HTML
- JavaScript
- Network Requests

### Match Examples
- AW-
- googleadservices.com
- google_conversion_id
- gtag('config','AW-...')

Output: Google Ads = Yes / No

Acceptance Criteria:
- Detect dynamically loaded tags.
- Never crash on detection failure.

---

## FR-009 Detect Meta Pixel

Match Examples
- fbq(
- connect.facebook.net
- fbevents.js

Output: Meta Pixel = Yes / No

---

## FR-010 Detect Microsoft UET

Match Examples
- bat.bing.com
- uetq

Output: Microsoft UET = Yes / No

---

## FR-011 Detect TikTok Pixel

Match Examples
- ttq.track
- analytics.tiktok.com

Output: TikTok Pixel = Yes / No

---

## FR-012 Detect LinkedIn Insight

Match Examples
- snap.licdn.com

Output: LinkedIn Insight = Yes / No

---

## FR-013 Detect Pinterest Tag

Match Examples
- pintrk
- ct.pinterest.com

Output: Pinterest Tag = Yes / No

---

# Combined Result Logic

If one or more supported technologies are detected:

**Result = Running Ads**

Otherwise:

**Result = No Evidence**

---

# False Positive Rules

- Ignore plain text mentions.
- Prefer executable scripts and network requests.
- Prefer multiple indicators before marking detected.

---

# Logging

Store:
- Domain
- Detected technologies
- Scan duration
- Retry count
- Error message

---

Next Document:
FUNCTIONAL_REQUIREMENTS_PART_3.md
