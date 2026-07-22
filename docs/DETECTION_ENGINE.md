# Detection Engine

## Project Name

Ads Detector

---

# 1. Overview

The Detection Engine is the intelligence layer of Ads Detector responsible for analyzing collected website data and identifying advertising, marketing, analytics, and tracking technologies.

The Detection Engine receives raw data from the Scanner Engine and converts it into meaningful intelligence.

The system analyzes:

- JavaScript files
- Network requests
- HTML elements
- Cookies
- Third-party domains
- Tracking identifiers

and determines which advertising technologies are active on a website.

---

# 2. Detection Engine Responsibilities

The Detection Engine is responsible for:

- Processing scanner output
- Running detection rules
- Identifying advertising platforms
- Collecting detection evidence
- Calculating confidence scores
- Reducing false positives
- Saving detection results

---

# 3. Detection Architecture

```
Scanner Engine

        |

        ↓

Raw Website Data

        |

        ↓

Detection Processor

        |

        ↓

Rule Matching Engine

        |

        ↓

Evidence Analyzer

        |

        ↓

Confidence Scoring

        |

        ↓

Database Storage
```

---

# 4. Detection Pipeline

The complete detection workflow:

```
Website Scanned

↓

Collect Scripts

↓

Analyze Requests

↓

Check Patterns

↓

Match Detection Rules

↓

Generate Evidence

↓

Calculate Confidence

↓

Save Result
```

---

# 5. Detection Input Data

The Detection Engine receives:

## HTML Data

Examples:

```
<script>

<meta>

iframe

tracking elements
```

---

## JavaScript Files

Examples:

```
gtag.js

fbq()

ttq()

analytics scripts
```

---

## Network Requests

Examples:

```
googleads.g.doubleclick.net

facebook.com/tr

analytics.tiktok.com
```

---

## Cookies

Examples:

```
_fbp

_ga

_gcl_au
```

---

# 6. Detection Methods

The system uses multiple detection methods.

---

## 6.1 Script Detection

The engine scans JavaScript resources.

Example:

Found:

```
gtag.js
```

Result:

```
Google Ads detected
```

---

## 6.2 Network Detection

The engine analyzes external requests.

Example:

Request:

```
connect.facebook.net
```

Result:

```
Meta Pixel detected
```

---

## 6.3 Cookie Detection

The engine checks browser cookies.

Example:

Cookie:

```
_fbp
```

Result:

```
Meta Pixel detected
```

---

## 6.4 HTML Pattern Detection

The engine checks page source.

Example:

```
<script src="facebook-pixel.js">
```

Result:

```
Facebook Tracking Found
```

---

# 7. Supported Detection Platforms

Initial supported platforms:

```
Google Ads

Google Analytics

Meta Pixel

TikTok Pixel

Microsoft Advertising

LinkedIn Insight Tag

Pinterest Tag

Snap Pixel
```

---

# 8. Google Ads Detection

Detection signals:

## Script Patterns

Examples:

```
gtag()

google_conversion

AW-
```

---

## Domains

Examples:

```
googleadservices.com

doubleclick.net
```

---

## Cookies

Examples:

```
_gcl_au
```

---

Detection Result:

```
Platform:

Google Ads

Confidence:

High
```

---

# 9. Meta Pixel Detection

Detection signals:

## JavaScript

Pattern:

```
fbq()
```

---

## Domains

Examples:

```
connect.facebook.net

facebook.com/tr
```

---

## Cookies

Examples:

```
_fbp

_fbc
```

---

Detection Result:

```
Platform:

Meta Pixel
```

---

# 10. TikTok Pixel Detection

Detection signals:

## JavaScript

Pattern:

```
ttq()
```

---

## Domains

```
analytics.tiktok.com
```

---

Detection Result:

```
TikTok Pixel Found
```

---

# 11. Microsoft UET Detection

Detection signals:

Scripts:

```
bat.js
```

Domain:

```
bat.bing.com
```

Result:

```
Microsoft Advertising Detected
```

---

# 12. LinkedIn Insight Detection

Detection signals:

Script:

```
snap.licdn.com
```

Domain:

```
linkedin.com
```

Result:

```
LinkedIn Insight Tag
```

---

# 13. Detection Rule System

Detection rules define how technologies are identified.

Example rule:

```
Rule ID:

META_PIXEL_001


Condition:

IF script contains fbq()


THEN:

Meta Pixel Detected
```

---

# 14. Rule Structure

Each rule contains:

```
Rule ID

Platform Name

Pattern Type

Pattern Value

Confidence Weight

Description
```

---

Example:

```json
{
"id":"META_PIXEL_001",
"platform":"Meta Pixel",
"type":"javascript",
"pattern":"fbq()",
"weight":90
}
```

---

# 15. Evidence System

Every detection must store evidence.

Evidence examples:

```
Matched Script

Matched Domain

Cookie Found

Network Request
```

---

Example:

```
Detection:

Google Ads


Evidence:

Found:

googleadservices.com
```

---

# 16. Confidence Calculation

Confidence is calculated using multiple signals.

Example:

```
Script Match

+

Network Match

+

Cookie Match

=

Final Confidence
```

---

Confidence levels:

```
90-100

High


60-89

Medium


Below 60

Low
```

---

# 17. False Positive Prevention

The system should avoid incorrect detection.

Methods:

- Require multiple signals
- Use confidence scoring
- Validate domains
- Ignore common unrelated scripts

---

Example:

Single match:

```
Low confidence
```

Multiple matches:

```
High confidence
```

---

# 18. Detection Database

Detection results are stored.

Table:

```
detections
```

Fields:

```
id

website_id

platform

evidence

confidence

created_at
```

---

# 19. Rule Management

Future versions should support:

- Add new platforms
- Update patterns
- Remove outdated rules
- AI-generated rules

---

# 20. Performance Optimization

The Detection Engine should:

- Process data efficiently
- Avoid duplicate analysis
- Cache detection rules
- Run parallel analysis

---

# 21. Security Considerations

The Detection Engine must:

- Validate incoming data
- Avoid executing unknown scripts
- Treat website content as untrusted

---

# 22. Future Improvements

Possible upgrades:

- AI-based detection
- Machine learning classification
- Automatic rule discovery
- Competitor technology analysis
- Technology recommendation system

---

# 23. Summary

The Detection Engine transforms raw website data into actionable advertising intelligence.

Complete flow:

```
Website Data

↓

Detection Rules

↓

Technology Identification

↓

Confidence Score

↓

Lead Intelligence
```

The Detection Engine is the brain of Ads Detector.
