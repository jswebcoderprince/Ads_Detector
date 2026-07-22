# AI Implementation Rules

## Project Name

Ads Detector

---

# 1. Overview

This document defines the rules and guidelines that AI coding assistants and developers must follow when implementing Ads Detector.

The purpose of this document is to ensure:

- Clean architecture
- Maintainable code
- Secure implementation
- Consistent development
- Long-term scalability

---

# 2. Core Development Principles

All implementations must follow:

## Modularity

Each feature should have a clear responsibility.

Example:

```
CSV Processing

Scanner Engine

Detection Engine

Database Layer
```

Each module should work independently.

---

## Maintainability

Code should be:

- Easy to understand
- Properly documented
- Easy to modify

---

## Scalability

New features should not require rewriting existing systems.

---

# 3. Architecture Rules

AI must follow the defined architecture.

Required flow:

```
User Interface

↓

Application Core

↓

Processing Modules

↓

Database

```

Do not create direct communication between unrelated modules.

---

# 4. Code Organization Rules

Code should follow:

```
src/

├── core

├── scanner

├── detection

├── database

├── csv_processor

├── export

└── utils
```

Each folder should contain related functionality only.

---

# 5. Database Rules

Database:

```
SQLite
```

Rules:

- Never store duplicate records
- Always use migrations for changes
- Maintain foreign keys
- Validate user input before saving

---

Before creating a new table:

Check:

```
Existing Tables

Relationships

Future Scalability
```

---

# 6. Scanner Engine Rules

The scanner must:

- Use isolated browser sessions
- Respect timeout limits
- Handle failures gracefully
- Never execute unsafe actions

Required:

```
Timeout

Retry

Logging

Error Recovery
```

---

# 7. Detection Engine Rules

Detection logic must be:

- Rule based
- Evidence driven
- Explainable

Every detection requires:

```
Technology Name

Detection Pattern

Evidence

Confidence Score
```

---

Bad:

```
Google Ads Found
```

Good:

```
Google Ads Found

Evidence:

googleadservices.com request detected

Confidence:

95%
```

---

# 8. AI Generated Code Rules

AI-generated code must:

- Follow existing structure
- Avoid unnecessary dependencies
- Include comments for complex logic
- Include error handling

---

Do not generate:

- Duplicate modules
- Unused files
- Random architecture changes

---

# 9. Feature Development Process

Every new feature should follow:

```
Requirement

↓

Design

↓

Implementation

↓

Testing

↓

Documentation
```

---

# 10. Security Rules

AI must always consider:

## File Security

Validate:

- File type
- File size
- File content

---

## Database Security

Prevent:

- SQL injection
- Data corruption

---

## Browser Security

Prevent:

- Unsafe execution
- Malicious downloads

---

# 11. Error Handling Rules

Every module must include:

```
Validation

Error Handling

Logging

Recovery
```

Never silently fail.

---

# 12. Testing Rules

Every new feature requires:

```
Unit Test

Integration Test

Manual Verification
```

---

Example:

New Detection Rule:

Must test:

```
Correct Detection

False Positive

False Negative
```

---

# 13. Dependency Rules

Before adding a new library:

Check:

- Is it necessary?
- Is it maintained?
- Does it increase complexity?

Prefer existing tools.

---

# 14. Documentation Rules

Every major change requires updating:

```
README.md

Relevant Documentation

Change Log
```

---

# 15. Naming Rules

Use clear names.

Good:

```
scan_manager.py

detection_rule.py
```

Bad:

```
test1.py

newfile.py
```

---

# 16. Performance Rules

AI implementation should consider:

- Memory usage
- Processing speed
- Database efficiency

Avoid:

- Unnecessary loops
- Duplicate processing
- Blocking operations

---

# 17. Large Dataset Rules

The system should support:

```
10,000+

100,000+

domains
```

Use:

- Queue processing
- Pagination
- Batch operations

---

# 18. UI Development Rules

User interface should prioritize:

- Simple workflow
- Clear feedback
- Progress visibility

Required:

```
Loading States

Error Messages

Success Messages
```

---

# 19. Change Management Rules

Before changing architecture:

Check:

```
Current Documentation

Existing Modules

Database Impact
```

---

Large changes require documentation updates.

---

# 20. AI Decision Making Rules

When multiple solutions exist:

Choose the solution that provides:

1. Simplicity
2. Reliability
3. Maintainability
4. Scalability

Avoid unnecessary complexity.

---

# 21. Deployment Rules

Before deployment:

Verify:

```
Database

Environment

Dependencies

Security

Testing
```

---

# 22. Future AI Improvements

Possible additions:

- AI generated detection rules
- Automatic bug analysis
- Smart lead scoring
- Website classification

---

# 23. Final Rule

The goal of every implementation is:

```
Simple

Reliable

Secure

Scalable

Maintainable
```

Every feature must improve Ads Detector without reducing system stability.
