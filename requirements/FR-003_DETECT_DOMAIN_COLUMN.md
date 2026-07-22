# FR-003: Domain Detection and Extraction

## Requirement ID

FR-003

---

## Requirement Name

Website Domain Detection and Extraction

---

# Purpose

The Domain Detection module identifies and extracts valid website domains from uploaded and validated CSV data.

The purpose of this module is to ensure that every website sent to the scanning engine has a clean and standardized domain format.

---

# Related User Stories

- US-002: Validate Uploaded CSV
- US-003: Normalize Domains
- US-004: Start Website Scan

---

# Functional Description

The system shall automatically extract website domains from user-provided data.

The module must support:

- Full URLs
- Domain-only inputs
- URLs with paths
- URLs with parameters
- Different domain formats

---

# Domain Detection Workflow

```
CSV Data

↓

Read Domain Values

↓

Extract URL Components

↓

Identify Root Domain

↓

Validate Domain

↓

Store Clean Domain

↓

Send To Scanner
```

---

# Supported Input Formats

The system should support:

## Full HTTPS URL

Example:

```
https://www.example.com
```

Output:

```
example.com
```

---

## Full HTTP URL

Example:

```
http://example.com
```

Output:

```
example.com
```

---

## WWW URL

Example:

```
www.example.com
```

Output:

```
example.com
```

---

## URL With Path

Example:

```
https://example.com/about/services
```

Output:

```
example.com
```

---

## URL With Parameters

Example:

```
https://example.com/page?id=123
```

Output:

```
example.com
```

---

# Domain Extraction Rules

The system must remove:

```
http://

https://

www.

/

?

#

parameters

fragments
```

---

# Root Domain Detection

The system should identify the main domain.

Examples:

Input:

```
shop.example.com
```

Output:

```
example.com
```

---

Input:

```
www.blog.example.co.uk
```

Output:

```
example.co.uk
```

---

# Subdomain Handling

The system should support subdomains.

Default behavior:

Convert:

```
www.example.com
```

to:

```
example.com
```

---

For business scanning:

The system should keep meaningful subdomains when required.

Example:

```
store.example.com
```

may be stored as:

```
store.example.com
```

while maintaining:

```
example.com
```

as the root domain.

---

# International Domain Support

The system should support:

- .com
- .org
- .net
- .io
- .co
- .ai
- Country domains

Examples:

```
example.co.uk

example.de

example.ca
```

---

# Domain Validation Rules

A valid domain should:

Contain:

- Domain name
- Valid extension

Examples:

Valid:

```
google.com

company.co.uk

startup.io
```

Invalid:

```
hello

example.

@test.com
```

---

# Duplicate Handling

After extraction:

The system should compare normalized domains.

Example:

Input:

```
https://example.com

www.example.com

example.com/page
```

Result:

```
example.com
```

Only one domain should continue to scanning.

---

# Domain Metadata

Each processed domain should store:

```
Original Value

Clean Domain

Root Domain

Status

Validation Result
```

Example:

```
Original:

https://www.example.com/about


Domain:

example.com


Status:

Valid
```

---

# Database Behavior

After successful extraction, the system may store:

- Original URL
- Clean domain
- Root domain
- Processing status

---

# Error Handling

## Invalid Domain

Message:

```
Invalid website domain detected.

This record will be skipped.
```

---

## Missing Domain

Message:

```
No website information found.
```

---

## Unsupported Format

Message:

```
The website format cannot be processed.
```

---

# Acceptance Criteria

The feature is complete when:

## AC-001

System extracts domains from URLs.

---

## AC-002

System removes unnecessary URL components.

---

## AC-003

System detects root domains correctly.

---

## AC-004

System supports different domain extensions.

---

## AC-005

System sends only clean domains to scanner.

---

# Future Improvements

Possible enhancements:

- Advanced WHOIS lookup
- Domain age detection
- Business category detection
- Country detection
- Domain authority analysis

---

# Summary

FR-003 ensures that every website entering the scanning engine follows a clean and consistent format.

A reliable domain extraction process improves:

- Scan accuracy
- Duplicate prevention
- Database consistency
- Export quality
