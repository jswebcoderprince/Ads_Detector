# CSV Processing Engine

## Project Name

Ads Detector

---

# 1. Overview

The CSV Processing Engine is responsible for handling user-uploaded domain files and preparing them for website scanning.

This engine manages:

- CSV upload
- File validation
- Data cleaning
- Duplicate removal
- Domain extraction
- Data normalization
- Scan queue preparation

The processed data is then transferred to the Scan Queue Manager.

---

# 2. Responsibilities

The CSV Processing Engine handles:

- Accepting CSV files
- Checking file structure
- Validating domain data
- Removing invalid records
- Removing duplicates
- Extracting clean domains
- Preparing scan-ready data

---

# 3. Processing Architecture

```
User Uploads CSV

        |

        ↓

File Validator

        |

        ↓

CSV Parser

        |

        ↓

Data Cleaner

        |

        ↓

Domain Processor

        |

        ↓

Scan Queue
```

---

# 4. Supported File Formats

Version 1:

```
CSV
```

Future support:

```
Excel (.xlsx)

JSON
```

---

# 5. CSV Upload Process

Workflow:

```
Select File

↓

Upload

↓

Validate

↓

Process Data

↓

Show Preview

↓

Start Scan
```

---

# 6. File Validation

Before processing, the system checks:

## File Extension

Allowed:

```
.csv
```

Rejected:

```
.exe

.zip

.unknown
```

---

## File Size

The system should limit upload size.

Example:

```
Maximum:

100 MB
```

---

## File Structure

The system checks:

- Header availability
- Column format
- Empty files
- Corrupted data

---

# 7. CSV Column Detection

The system should automatically detect common columns.

Supported names:

```
domain

website

url

domain_name
```

---

Example:

Input:

```
website

example.com
test.com
```

Output:

```
Domain:

example.com

test.com
```

---

# 8. Domain Extraction

The engine extracts clean domains.

Examples:

Input:

```
https://www.example.com/page
```

Output:

```
example.com
```

---

# 9. Data Cleaning

Cleaning operations:

## Remove Empty Rows

Example:

Before:

```
example.com

(empty)

test.com
```

After:

```
example.com

test.com
```

---

## Remove Invalid Domains

Invalid:

```
abc

12345

random text
```

---

## Remove Duplicates

Before:

```
example.com

example.com

test.com
```

After:

```
example.com

test.com
```

---

# 10. Domain Normalization

The system normalizes domains.

Rules:

Remove:

```
www.

http://

https://

/
```

Convert:

```
Example.COM
```

to:

```
example.com
```

---

# 11. Preview System

Before scanning, user should see:

Example:

```
Total Uploaded:

1000


Valid Domains:

950


Removed:

50
```

---

# 12. Processing Result

After processing:

The system generates:

```
Clean Domain List

Invalid Records

Duplicate Records

Processing Report
```

---

# 13. Scan Queue Integration

Processed domains are sent to:

```
Scan Queue Manager
```

Example:

Input:

```
950 domains
```

Queue:

```
Pending:

950
```

---

# 14. Database Storage

Processed data is stored.

Tables:

```
websites

scan_sessions

scan_queue
```

---

# 15. Error Handling

## Invalid CSV

Message:

```
Unable to process this CSV file.
Please upload a valid file.
```

---

## Empty File

Message:

```
CSV file contains no data.
```

---

## No Valid Domains

Message:

```
No valid domains found.
```

---

# 16. Performance Requirements

The engine should support:

```
100,000+ domains
```

Requirements:

- Streaming processing
- Memory optimization
- Background processing

---

# 17. Security Considerations

The system should:

- Validate uploaded files
- Prevent CSV injection
- Sanitize input data
- Limit file size

---

# 18. Future Improvements

Possible upgrades:

- Automatic column mapping
- AI domain classification
- Country detection
- Industry detection
- Lead quality prediction

---

# 19. Summary

The CSV Processing Engine converts raw uploaded files into clean scanning tasks.

Complete workflow:

```
Raw CSV

↓

Validation

↓

Cleaning

↓

Domain Extraction

↓

Scan Queue

↓

Website Scanner
```

This module ensures Ads Detector starts every scan with accurate and reliable data.
