# FR-015: Notes and Tag Management

## Requirement ID

FR-015

---

## Requirement Name

Prospect Notes and Tag Organization System

---

# Purpose

The Notes and Tag Management module allows users to organize scanned websites by adding custom information and categories.

The purpose of this module is to help users manage prospects efficiently after detection.

---

# Related User Stories

- US-013: Add Notes
- US-014: Add Tags
- US-015: Manage Prospect Lists

---

# Functional Description

The system shall allow users to attach:

- Personal notes
- Custom tags
- Sales status labels

to any scanned website.

These details should remain saved permanently.

---

# Workflow

```
Scan Result

↓

Open Website Details

↓

Add Note / Tag

↓

Save Information

↓

Manage Prospect Later
```

---

# Notes System

## Purpose

Notes allow users to store important information about a prospect.

---

# Adding Notes

Users should be able to add notes from:

- Result table
- Website details page
- Starred prospects page

---

# Example Notes

```
Website has Google Ads but poor landing page.

Need redesign proposal.

Contact owner next Monday.
```

---

# Note Structure

Each note should contain:

```
Note ID

Website ID

Note Content

Created Date

Updated Date
```

---

# Multiple Notes Support

A single website can have multiple notes.

Example:

```
example.com


Note 1:

Initial audit completed.


Note 2:

Sent proposal.
```

---

# Edit Notes

Users should be able to:

- Update existing notes
- Delete unwanted notes

---

# Tag System

## Purpose

Tags help users categorize and organize prospects.

---

# Default Tags

The system should include:

```
Hot Lead

Warm Lead

Follow Up

Contacted

Interested

Not Interested

Client
```

---

# Custom Tags

Users should be able to create their own tags.

Example:

```
Roofing Campaign

USA Leads

July Outreach
```

---

# Tag Workflow

```
Select Website

↓

Choose Tag

↓

Save

↓

Filter By Tag
```

---

# Multiple Tag Support

One website can have multiple tags.

Example:

```
example.com


Tags:

Hot Lead

USA

Follow Up
```

---

# Tag Management

Users should be able to:

- Create tags
- Rename tags
- Delete tags
- Assign tags
- Remove tags

---

# Sales Workflow Example

Example:

```
New Prospect Found

↓

Tag:

New Lead


↓

Contact Sent

↓

Tag:

Contacted


↓

Interested

↓

Tag:

Potential Client
```

---

# Database Requirements

## Notes Table

```
notes
```

Fields:

```
id

website_id

note_text

created_at

updated_at
```

---

## Tags Table

```
tags
```

Fields:

```
id

tag_name

created_at
```

---

## Website Tags Table

```
website_tags
```

Fields:

```
id

website_id

tag_id
```

---

# Search Integration

Users should be able to search:

- Websites with specific tags
- Websites containing specific notes

Example:

Search:

```
Follow Up
```

Result:

```
All follow-up prospects
```

---

# Filtering Integration

Tags should work with filtering system.

Example:

Filter:

```
Tag:

Hot Lead
```

Result:

```
Only hot prospects
```

---

# Export Integration

Export files should include:

```
Tags

Notes
```

Example CSV:

```
domain,

ads,

score,

tags,

notes
```

---

# User Interface Requirements

Notes and tags should be accessible from:

## Result Table

Quick actions:

```
Add Note

Add Tag
```

---

## Website Details

Full management:

```
Notes History

Assigned Tags
```

---

## Dashboard

Statistics:

```
Hot Leads

Follow Ups

Contacted
```

---

# Error Handling

## Note Save Failed

Message:

```
Unable to save note.
Please try again.
```

---

## Tag Creation Failed

Message:

```
Unable to create tag.
```

---

# Performance Requirements

The system should support:

```
100,000+ notes

50,000+ tags
```

Requirements:

- Indexed searches
- Fast loading
- Efficient database queries

---

# Acceptance Criteria

The feature is complete when:

## AC-001

Users can add notes to websites.

---

## AC-002

Users can edit and delete notes.

---

## AC-003

Users can create custom tags.

---

## AC-004

Users can assign multiple tags.

---

## AC-005

Tags and notes appear in exports.

---

## AC-006

Information remains after application restart.

---

# Future Improvements

Possible enhancements:

- Follow-up reminders
- CRM pipeline
- Email integration
- AI-generated notes
- Automatic lead categorization

---

# Summary

FR-015 transforms Ads Detector from a simple scanning tool into a complete prospect management system.

Users can move from:

```
Website Detection
```

to:

```
Organized Sales Pipeline
```

by adding notes, tags, and follow-up information.
