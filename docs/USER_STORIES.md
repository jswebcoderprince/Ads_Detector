# User Stories

## Overview

This document defines the main user interactions and expectations for Ads Detector.

Each user story describes:

- Who is using the system
- What they want to accomplish
- Why they need it
- What success looks like

Format:

```
As a [user type]

I want to [action]

So that [benefit]
```

---

# User Roles

Ads Detector mainly supports the following user types:

## Agency Owner

A person managing a web design, marketing, SEO, or lead generation agency.

---

## Lead Generation Specialist

A person responsible for finding qualified business prospects.

---

## Digital Marketer

A person researching businesses and marketing activities.

---

## Freelancer

An independent professional searching for potential clients.

---

# CSV Management Stories

---

## US-001: Upload Website List

### Story

As a user,

I want to upload a CSV file containing website domains,

so that I can scan multiple websites automatically instead of checking them manually.

### Acceptance Criteria

- User can upload CSV files.
- System accepts valid CSV formats.
- System detects domain columns automatically.
- System shows upload success status.
- Invalid files show error messages.

---

# US-002: Validate Uploaded CSV

### Story

As a user,

I want the system to validate my CSV before scanning,

so that incorrect data does not create scanning errors.

### Acceptance Criteria

The system should:

- Check required columns.
- Detect empty rows.
- Remove invalid domains.
- Identify duplicate domains.
- Show validation summary.

---

# US-003: Normalize Domains

### Story

As a user,

I want the system to automatically clean website URLs,

so that different URL formats are treated as the same website.

### Example

Input:

```
https://www.example.com/page
```

Output:

```
example.com
```

---

# Website Scanning Stories

---

## US-004: Start Website Scan

### Story

As a user,

I want to start scanning uploaded domains,

so that the system can automatically analyze websites.

### Acceptance Criteria

The system should:

- Create scan queue.
- Process websites automatically.
- Show scan progress.
- Display current scanning domain.

---

# US-005: Monitor Scan Progress

### Story

As a user,

I want to see scanning progress,

so that I know how much work is completed.

### The interface should show:

- Total domains
- Completed domains
- Remaining domains
- Current domain
- Estimated completion time

---

# US-006: Handle Failed Websites

### Story

As a user,

I want failed scans to be recorded,

so that I can review or retry them later.

### Failed cases include:

- Timeout
- SSL error
- DNS failure
- Website unavailable
- Browser error

---

# Advertising Detection Stories

---

## US-007: Detect Advertising Technologies

### Story

As a user,

I want the system to detect advertising technologies,

so that I can identify businesses investing in digital marketing.

### The system should detect:

- Google Ads
- Meta Pixel
- Microsoft UET
- TikTok Pixel
- LinkedIn Insight
- Pinterest Tag

---

# US-008: Understand Detection Results

### Story

As a user,

I want to understand why a website was marked as running ads,

so that I can trust the results.

### Each result should include:

- Detection status
- Detection confidence
- Detection method
- Detection reason

---

# US-009: View Prospect Score

### Story

As a user,

I want websites to receive a prospect score,

so that I can prioritize valuable leads.

### Example:

```
Website A

Score: 95/100

Reason:

Multiple advertising platforms detected
```

---

# Result Management Stories

---

## US-010: Search Results

### Story

As a user,

I want to search scanned websites,

so that I can quickly find specific prospects.

### Search fields:

- Domain
- Notes
- Tags

---

# US-011: Filter Results

### Story

As a user,

I want to filter scan results,

so that I can focus only on valuable prospects.

### Filters:

- Google Ads detected
- Meta detected
- Confidence level
- Prospect score
- Scan status
- Starred prospects

---

# US-012: Star Important Prospects

### Story

As a user,

I want to star important websites,

so that I can easily find my best prospects later.

---

# US-013: Add Notes

### Story

As a user,

I want to add notes to prospects,

so that I can remember sales information.

### Example:

```
Needs website redesign

Follow up next week
```

---

# US-014: Add Tags

### Story

As a user,

I want to organize prospects with tags,

so that I can manage my workflow.

### Example Tags:

- Hot Lead
- Follow Up
- Contacted
- High Value

---

# Export Stories

---

## US-015: Export All Results

### Story

As a user,

I want to export all scan results,

so that I can use the data externally.

---

## US-016: Export Filtered Results

### Story

As a user,

I want to export only filtered results,

so that unrelated websites are not included.

### Example:

```
1000 websites scanned

Filter:

Google Ads = YES

Confidence = HIGH


Export:

Only matching websites
```

---

## US-017: Export Selected Results

### Story

As a user,

I want to manually select websites,

so that I can export only chosen prospects.

---

## US-018: Export Starred Results

### Story

As a user,

I want to export starred prospects,

so that I can create targeted outreach lists.

---

# Database Stories

---

## US-019: View Scan History

### Story

As a user,

I want previous scans saved,

so that I can review historical data.

---

## US-020: Save Application Settings

### Story

As a user,

I want my settings saved,

so that I do not configure the application every time.

---

# Dashboard Stories

---

## US-021: View Statistics

### Story

As a user,

I want dashboard statistics,

so that I can understand my scanning activity.

### Statistics:

- Total scans
- Total websites
- Ads detected
- Average confidence
- Scan duration

---

# Future User Stories

The following stories are planned for future versions:

- AI website analysis
- CRM integration
- Automated outreach
- Team collaboration
- Cloud synchronization

---

# Summary

The user experience of Ads Detector should allow users to:

```
Upload

↓

Scan

↓

Detect

↓

Analyze

↓

Organize

↓

Export

↓

Generate Leads
```

The system should minimize manual research and maximize qualified prospect discovery.
