# API Specification

## Project Name

Ads Detector

---

# 1. Overview

This document defines the internal API structure and communication rules between different components of Ads Detector.

The API layer provides a standardized way for modules to communicate with each other.

Main API responsibilities:

- Manage scan requests
- Control scanner operations
- Retrieve results
- Handle exports
- Manage application data

---

# 2. API Architecture

```
User Interface

        |

        |

Application API Layer

        |

 -------------------------

 |        |        |       |

Scan   Result   Export  Settings

API     API      API      API

        |

        |

Database Layer
```

---

# 3. API Design Principles

The API should follow:

## Simplicity

Easy communication between modules.

---

## Consistency

All requests and responses follow standard formats.

---

## Error Handling

Every API returns clear error messages.

---

## Future Ready

Structure should support external API access.

---

# 4. Common Response Format

All APIs should return:

```json
{
    "status": "success",
    "message": "Operation completed",
    "data": {}
}
```

---

# Error Response

Example:

```json
{
    "status": "error",
    "message": "Unable to process request",
    "error_code": "SCAN_FAILED"
}
```

---

# 5. Scan API

## Create New Scan

Purpose:

Create a scanning session.

---

Endpoint:

```
POST /api/scans
```

---

Request:

```json
{
    "scan_name": "USA Roofing Campaign",
    "file": "domains.csv"
}
```

---

Response:

```json
{
    "status": "success",
    "scan_id": "SCAN-001",
    "message": "Scan created"
}
```

---

# Get Scan Status

Purpose:

Check scanning progress.

---

Endpoint:

```
GET /api/scans/{scan_id}
```

---

Response:

```json
{
    "scan_id": "SCAN-001",
    "status": "processing",
    "total":1000,
    "completed":450
}
```

---

# Start Scan

Endpoint:

```
POST /api/scans/{scan_id}/start
```

---

Response:

```json
{
    "status":"success",
    "message":"Scan started"
}
```

---

# Stop Scan

Endpoint:

```
POST /api/scans/{scan_id}/stop
```

---

Response:

```json
{
    "status":"success",
    "message":"Scan stopped"
}
```

---

# 6. Website API

## Add Website

Endpoint:

```
POST /api/websites
```

---

Request:

```json
{
    "domain":"example.com"
}
```

---

Response:

```json
{
    "website_id":1001,
    "status":"added"
}
```

---

# Get Website Details

Endpoint:

```
GET /api/websites/{id}
```

---

Response:

```json
{
    "domain":"example.com",
    "ads_detected":true,
    "platforms":[
        "Google Ads"
    ],
    "confidence":95
}
```

---

# 7. Detection API

## Run Detection

Purpose:

Analyze website data.

Endpoint:

```
POST /api/detection/run
```

---

Request:

```json
{
    "website_id":1001
}
```

---

Response:

```json
{
    "detected":true,
    "technologies":[
        "Meta Pixel",
        "Google Ads"
    ]
}
```

---

# 8. Results API

## Get Results

Endpoint:

```
GET /api/results
```

---

Query:

```
?page=1
&limit=50
```

---

Response:

```json
{
    "total":1000,
    "results":[
        {
            "domain":"example.com",
            "score":90
        }
    ]
}
```

---

# Filter Results

Endpoint:

```
POST /api/results/filter
```

---

Request:

```json
{
    "ads_detected":true,
    "min_score":80
}
```

---

Response:

```json
{
    "filtered_results":200
}
```

---

# 9. Export API

## Create Export

Endpoint:

```
POST /api/export
```

---

Request:

```json
{
    "type":"csv",
    "filter":"starred"
}
```

---

Response:

```json
{
    "file":"results.csv",
    "status":"ready"
}
```

---

# 10. Notes API

## Add Note

Endpoint:

```
POST /api/notes
```

---

Request:

```json
{
    "website_id":1001,
    "note":"Need follow up"
}
```

---

Response:

```json
{
    "status":"saved"
}
```

---

# 11. Tags API

## Add Tag

Endpoint:

```
POST /api/tags
```

---

Request:

```json
{
    "website_id":1001,
    "tag":"Hot Lead"
}
```

---

Response:

```json
{
    "status":"added"
}
```

---

# 12. Settings API

## Get Settings

Endpoint:

```
GET /api/settings
```

---

Response:

```json
{
    "timeout":30,
    "concurrency":5
}
```

---

## Update Settings

Endpoint:

```
PUT /api/settings
```

---

Request:

```json
{
    "timeout":60
}
```

---

# 13. Notification API

## Get Notifications

Endpoint:

```
GET /api/notifications
```

---

Response:

```json
{
    "notifications":[
        {
            "message":"Scan completed"
        }
    ]
}
```

---

# 14. Database Communication

All APIs communicate with:

```
SQLite Database
```

Main entities:

```
Users

Scans

Websites

Results

Notes

Tags

Exports

Notifications
```

---

# 15. API Security

Requirements:

- Validate all inputs
- Prevent unauthorized access
- Sanitize uploaded files
- Protect database operations

---

# 16. Future External API Support

Future versions may expose:

```
Public API

API Keys

Webhooks

CRM Integration
```

---

# 17. Summary

The API layer creates a clean communication system between Ads Detector components.

Architecture:

```
Frontend

↓

API Layer

↓

Core Modules

↓

Database
```

This allows Ads Detector to evolve from a local application into a scalable intelligence platform.
