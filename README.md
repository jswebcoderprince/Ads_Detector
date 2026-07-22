# 🚀 Ads Detector

> A professional local web application that scans websites from a CSV file and detects advertising technologies such as Google Ads, Meta Pixel, Microsoft UET, TikTok Pixel, LinkedIn Insight, and Pinterest Tag.

---

# Overview

Ads Detector is a desktop-first local web application designed for agencies, marketers, lead generation professionals, and cold email outreach teams.

The application allows users to upload a CSV file containing website domains. It automatically visits each website using Playwright, analyzes its advertising technologies, and generates a detailed report with confidence scoring and export options.

Unlike simple tag checkers, Ads Detector is designed to become a complete prospect intelligence platform that helps users identify businesses actively investing in digital marketing.

---

# Core Features

## CSV Processing

- Upload CSV files containing website domains
- Automatic domain column detection
- Domain normalization
- Duplicate removal
- CSV validation
- Scan queue generation

---

## Website Scanner

- Automated browser scanning using Playwright
- JavaScript rendering support
- Dynamic website detection
- Network request monitoring
- Background scanning
- Parallel processing

---

## Advertising Technology Detection

Supports detection of:

- Google Ads
- Google Conversion Tracking
- Meta Pixel
- Microsoft UET
- TikTok Pixel
- LinkedIn Insight Tag
- Pinterest Tag

---

## Detection Intelligence

Every scanned website includes:

- Detection Status
- Detection Confidence
- Detection Method
- Detection Reason
- Prospect Score
- Platform Count
- Scan Status

---

## Prospect Management

Users can:

- ⭐ Star prospects
- 📝 Add notes
- 🏷 Add custom tags
- Search domains
- Filter results
- Sort results
- Save prospect history

---

## Smart Filtering

Filter results by:

- Google Ads
- Meta Pixel
- TikTok Pixel
- LinkedIn
- Microsoft UET
- Pinterest
- Detection Confidence
- Prospect Score
- Scan Status
- Starred Prospects

---

## Export Options

Export:

- All Results
- Filtered Results
- Selected Results
- Starred Results
- Failed Scans

Supported formats:

- CSV
- Excel
- JSON

---

# Dashboard

The dashboard provides:

- Total Scans
- Total Websites
- Ads Detected
- Average Confidence
- Scan Duration
- Recent Activity
- Previous Scan History

---

# Local Database

Ads Detector uses SQLite.

The database stores:

- Scan History
- Scan Results
- Application Settings
- Notes
- Tags
- Starred Prospects
- Statistics

No external database server is required.

---

# Technology Stack

## Frontend

- React
- Vite
- Tailwind CSS
- shadcn/ui

## Backend

- Python
- FastAPI

## Browser Automation

- Playwright

## Database

- SQLite
- SQLAlchemy

## CSV Engine

- Pandas

---

# Typical Workflow

```text
Upload CSV

↓

Validate CSV

↓

Create Scan Queue

↓

Launch Playwright

↓

Visit Website

↓

Detect Advertising Technologies

↓

Calculate Confidence

↓

Generate Prospect Score

↓

Store Results

↓

Search / Filter

↓

Export Results
```

---

# Project Structure

```text
ads-detector-docs/

docs/
requirements/
diagrams/
examples/
prompts/
assets/
```

---

# Documentation

Project documentation is organized into multiple sections.

## Business Documentation

- Product Vision
- Project Scope
- Business Requirements
- User Stories

## Functional Requirements

FR-001 through FR-020

## Technical Documentation

- System Architecture
- Detection Engine
- Scanner Engine
- API Specification
- CSV Processing Engine
- Playwright Engine

---

# Roadmap

## Version 1

- Local Desktop Web App
- CSV Upload
- Website Scanner
- Ads Detection
- SQLite Database
- Dashboard
- Export System

## Version 2

- AI Detection Improvements
- Better Confidence Scoring
- Additional Marketing Technology Detection
- Resume Scans
- Scheduled Scans

## Version 3

- AI Prospect Analysis
- Website Quality Scoring
- Conversion Opportunity Analysis
- Team Workspace
- Cloud Synchronization

---

# License

This project is licensed under the MIT License.

---

# Contributing

Contributions, feature suggestions, and improvements are welcome.

Please read CONTRIBUTING.md before submitting pull requests.

---

# Status

🚧 Documentation in Progress

Current Version: 1.0 Documentation

Project Type:

Local Desktop Web Application

Development Status:

Planning & Documentation Phase
