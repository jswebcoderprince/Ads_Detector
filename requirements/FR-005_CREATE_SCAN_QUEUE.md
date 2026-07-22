# FR-005: Scan Queue Management

## Requirement ID

FR-005

---

## Requirement Name

Website Scan Queue Management

---

# Purpose

The Scan Queue Management module controls how website scanning tasks are organized, processed, monitored, and completed.

The purpose of this module is to ensure efficient scanning of multiple websites while maintaining system stability and providing accurate progress tracking.

---

# Related User Stories

- US-004: Start Website Scan
- US-005: Monitor Scan Progress
- US-006: Handle Failed Websites
- US-019: View Scan History

---

# Functional Description

After creating a scan session, the system shall generate a queue containing all validated domains.

Each domain will become an individual scanning task with its own status and processing information.

---

# Queue Workflow

```
Validated Domains

↓

Create Queue Items

↓

Assign Status

↓

Process Pending Tasks

↓

Send To Scanner Engine

↓

Update Results

↓

Complete Queue
```

---

# Queue Item Structure

Each website in the queue should contain:

| Field | Description |
|---|---|
| Queue ID | Unique task identifier |
| Scan ID | Related scan session |
| Domain | Website domain |
| Status | Current task status |
| Priority | Processing priority |
| Retry Count | Number of retries |
| Created Time | Queue creation time |
| Started Time | Scan start time |
| Completed Time | Completion time |

---

# Queue Status

Each task can have the following states:

```
Pending

↓

Processing

↓

Completed

OR

Failed

↓

Retry Pending

↓

Completed / Failed
```

---

# Initial Queue Creation

When a scan starts:

Example:

Input:

```
1000 domains
```

System creates:

```
1000 queue items
```

Each item starts with:

```
Status:

Pending
```

---

# Processing Logic

The queue manager should:

1. Pick pending tasks.
2. Send domains to scanner engine.
3. Monitor execution.
4. Receive results.
5. Update task status.
6. Continue until queue completion.

---

# Concurrency Management

The system should control how many websites are scanned simultaneously.

Example:

Low:

```
2 websites at a time
```

Medium:

```
5 websites at a time
```

High:

```
10 websites at a time
```

The limit should depend on:

- User machine capability
- Available memory
- Browser resources

---

# Priority System

Version 1 supports basic priority.

Default:

All domains:

```
Normal Priority
```

Future support:

```
High Priority

Normal Priority

Low Priority
```

---

# Retry Management

Failed websites should support retry.

Retry cases:

- Timeout
- Temporary network failure
- Browser crash

---

# Retry Rules

Default:

```
Maximum Retry:

3 attempts
```

Example:

```
Attempt 1

Failed


Attempt 2

Failed


Attempt 3

Failed


Final Status:

Failed
```

---

# Failed Queue Handling

Failed domains should not stop the entire scan.

Example:

```
1000 Websites


Completed:

950


Failed:

50


Scan Status:

Completed
```

---

# Pause and Cancel Support

Future-ready design should support:

## Pause

Temporarily stop new scanning tasks.

Existing tasks may finish.

---

## Cancel

Stop the current scan session.

Remaining pending tasks become:

```
Cancelled
```

---

# Progress Calculation

The system should calculate:

## Completion Percentage

Formula:

```
Completed Domains

÷

Total Domains

×

100
```

---

Example:

```
500 completed

1000 total


Progress:

50%
```

---

# Database Storage

Queue information should be stored locally.

Recommended table:

```
scan_queue
```

Fields:

```
id

scan_id

domain

status

retry_count

priority

created_at

started_at

completed_at
```

---

# User Interface Requirements

The scan screen should display:

```
Scanning:

245 / 1000


Completed:

230


Failed:

15


Remaining:

755
```

---

# Error Handling

## Queue Creation Failed

Message:

```
Unable to create scan queue.

Please try again.
```

---

## Queue Empty

Message:

```
No websites available for scanning.
```

---

## Processing Error

Message:

```
A scanning task failed.

The system will continue with remaining websites.
```

---

# Performance Requirements

The queue system should:

- Handle 1000+ tasks
- Avoid loading all browser sessions at once
- Prevent memory overflow
- Maintain accurate progress

---

# Acceptance Criteria

The feature is complete when:

## AC-001

System creates queue items from validated domains.

---

## AC-002

Each domain has an individual status.

---

## AC-003

System processes multiple websites safely.

---

## AC-004

Failed websites do not stop the complete scan.

---

## AC-005

System supports retry handling.

---

## AC-006

Progress updates correctly during scanning.

---

# Future Improvements

Possible enhancements:

- Smart priority queue
- AI-based scan ordering
- Resume interrupted scans
- Distributed scanning
- Cloud worker support

---

# Summary

FR-005 defines how Ads Detector manages large-scale website scanning tasks.

A reliable queue system ensures:

- Stable performance
- Accurate progress tracking
- Failure recovery
- Scalable scanning capability

The Scan Queue Management module acts as the bridge between scan sessions and the website detection engine.
