# Ads Detector PRD v2 - Architecture & Technical Specification

## 1. System Architecture

Frontend (React) \| FastAPI Backend \| Scan Manager \| Playwright Worker
Pool \| Target Websites

## 2. Modules

### Frontend

-   Upload page
-   Progress page
-   Results table
-   Download button

### Backend

-   upload.py
-   scan.py
-   progress.py
-   export.py

### Scanner

-   browser_manager.py
-   worker.py
-   detector.py
-   parser.py

## 3. Folder Structure

    ads-detector/
      frontend/
      backend/
        api/
        scanner/
        services/
        models/
      uploads/
      reports/

## 4. API Specification

### POST /upload

Accepts CSV.

Response:

    {
      "job_id":"uuid",
      "rows":250
    }

### POST /scan

Body:

    {
      "job_id":"uuid",
      "concurrency":5
    }

### GET /progress/{job_id}

Returns completed, running, failed, total.

### GET /download/{job_id}

Downloads final CSV.

## 5. Detection Engine

Search rendered HTML, scripts and network requests.

Google Ads: - AW- - googleadservices.com - google_conversion_id

Meta: - fbq( - fbevents.js - connect.facebook.net

Microsoft: - bat.bing.com

TikTok: - ttq.track

LinkedIn: - snap.licdn.com

Pinterest: - pintrk

## 6. Worker Rules

-   Reuse browser instance.
-   One context per website.
-   Timeout 30s.
-   Retry once.
-   Close context after scan.

## 7. Result Logic

If any supported ad technology is detected:

Result = Running Ads

Else:

Result = No Evidence

## 8. Logging

Store: - Domain - Start time - Finish time - Errors - Retry count

## 9. Coding Rules

-   Python type hints required.
-   Modular architecture.
-   No business logic inside API routes.
-   Separate detector from scanner.

## 10. Milestones

1.  Upload
2.  Scanner
3.  Detection
4.  Progress
5.  Export
6.  UI polish
