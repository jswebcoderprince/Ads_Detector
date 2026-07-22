# System Architecture

## Project Name

Ads Detector

---

# 1. Overview

Ads Detector is a website intelligence application that scans domains and identifies advertising technologies running on websites.

The system allows users to:

- Upload domain lists
- Scan websites
- Detect advertising technologies
- Calculate confidence scores
- Organize prospects
- Filter results
- Export qualified leads

The architecture is designed to support large-scale website scanning while maintaining performance, security, and data ownership.

---

# 2. Architecture Goals

The system is designed around the following principles:

## Performance

The application should process thousands of domains efficiently.

---

## Reliability

Failed scans should not stop the entire scanning process.

---

## Security

External websites must be scanned safely.

---

## Scalability

The architecture should support future expansion.

---

## Data Ownership

User data remains locally controlled.

---

# 3. High-Level Architecture

```
                User

                 |

                 |

          Application UI

                 |

                 |

          Application Core

                 |

     -------------------------

     |           |           |

 Scanner   Detection    Database

 Engine     Engine      Layer


                 |

                 |

            Export System

```

---

# 4. Main Components

The system consists of:

```
Frontend / User Interface

Application Core

CSV Processing Module

Scanner Engine

Detection Engine

Scoring Engine

Database Layer

Export Module

Notification System
```

---

# 5. Application Structure

```
Ads Detector

│
├── User Interface
│
├── Core Application
│
├── Scanner Engine
│
├── Detection Engine
│
├── Database
│
├── Export System
│
└── Configuration
```

---

# 6. User Interface Layer

## Responsibility

The UI provides interaction between users and the system.

Main sections:

```
Dashboard

CSV Upload

Scan Management

Results

Filters

Exports

Settings
```

---

# 7. Application Core

## Responsibility

The application core controls communication between modules.

Responsibilities:

- Manage workflow
- Handle user actions
- Coordinate scanning
- Manage application state

---

# 8. CSV Processing Module

## Responsibility

Processes uploaded domain files.

Functions:

- Validate files
- Remove duplicates
- Extract domains
- Create scanning queue

Flow:

```
CSV Upload

↓

Validation

↓

Domain Extraction

↓

Scan Queue
```

---

# 9. Scanner Engine

## Responsibility

The Scanner Engine visits websites and collects technical information.

Tasks:

- Open website
- Load resources
- Execute JavaScript
- Capture network activity
- Collect evidence

Flow:

```
Domain

↓

Secure Browser

↓

Website Loading

↓

Data Collection

↓

Detection Engine
```

---

# 10. Detection Engine

## Responsibility

Analyzes collected website data and identifies advertising technologies.

Detects:

```
Google Ads

Meta Pixel

TikTok Pixel

Microsoft UET

LinkedIn Insight

Other Tracking Systems
```

---

# 11. Confidence Scoring Engine

## Responsibility

Calculates detection reliability.

Example:

```
Detection Evidence

+

Technology Match

+

Network Signals

=

Confidence Score
```

Output:

```
High

Medium

Low
```

---

# 12. Database Layer

## Technology

SQLite Database

File:

```
ads_detector.db
```

Stores:

- Scan history
- Domains
- Results
- Scores
- Tags
- Notes
- Settings

---

# 13. Data Flow Architecture

```
User Uploads CSV

        |

        ↓

CSV Validator

        |

        ↓

Scan Queue

        |

        ↓

Scanner Engine

        |

        ↓

Detection Engine

        |

        ↓

Confidence Scoring

        |

        ↓

Database

        |

        ↓

Results Dashboard

        |

        ↓

Export
```

---

# 14. Queue Management System

The queue system manages large scanning tasks.

Example:

Input:

```
10,000 domains
```

Queue:

```
Pending

Processing

Completed

Failed
```

Benefits:

- Prevent system overload
- Resume failed scans
- Track progress

---

# 15. Security Architecture

External websites are treated as untrusted sources.

Protection:

- Browser isolation
- Timeout limits
- Resource limits
- Safe file handling

---

# 16. Storage Architecture

Local storage:

```
Application

↓

SQLite Database

↓

User Files
```

No external server dependency is required for version 1.

---

# 17. Technology Stack

## Frontend

Options:

- React
- Electron UI
- Desktop UI Framework

---

## Backend/Core

Options:

- Python
- Node.js

---

## Database

```
SQLite
```

---

## Browser Automation

Options:

- Playwright
- Puppeteer
- Selenium

---

# 18. Error Handling Architecture

Every module should handle failures independently.

Example:

```
Website A Failed

↓

Continue Scanning

↓

Save Error

↓

Notify User
```

---

# 19. Future Expansion

Possible upgrades:

- Cloud scanning
- Team accounts
- API access
- CRM integration
- AI prospect analysis
- Distributed scanning

---

# 20. Summary

Ads Detector follows a modular architecture where each component has a specific responsibility.

The complete system flow:

```
Upload Domains

↓

Process Data

↓

Scan Websites

↓

Detect Ads

↓

Score Prospects

↓

Organize Results

↓

Export Leads
```

This architecture allows Ads Detector to grow from a local scanning tool into a complete website intelligence platform.
