# Ads Detector

A website intelligence platform that analyzes domains and detects advertising, tracking, and marketing technologies installed on websites.

Ads Detector helps users identify:

- Advertising platforms
- Tracking pixels
- Analytics technologies
- Marketing tools
- Website intelligence signals

The system converts raw website data into actionable insights.

---

# 🚀 Features

## CSV Domain Processing

Upload thousands of domains and prepare them for scanning.

Features:

- CSV upload
- Domain validation
- Duplicate removal
- Data cleaning
- Scan queue preparation


---

## Website Scanner

Automatically analyze websites.

The scanner collects:

- HTML data
- JavaScript files
- Network requests
- Cookies
- Third-party resources


---

## Advertising Technology Detection

Detect installed technologies:

Supported:

- Google Ads
- Google Analytics
- Meta Pixel
- TikTok Pixel
- Microsoft Advertising
- LinkedIn Insight Tag
- Pinterest Tag
- Snap Pixel


---

## Result Management

Manage detected websites:

- View results
- Filter data
- Star important prospects
- Add notes
- Add tags
- Export selected results


---

## Local Database

Uses:

```
SQLite
```

Stores:

- Scan history
- Website records
- Detection results
- Notes
- Tags
- Settings


---

# 🏗️ System Architecture

High-level workflow:

```
CSV Upload

↓

CSV Processing Engine

↓

Scan Queue

↓

Scanner Engine

↓

Detection Engine

↓

Database

↓

Results Dashboard

↓

Export
```

---

# 📂 Project Structure

```
Ads_Detector/

│
├── requirements/
│
├── docs/
│
├── diagrams/
│
├── assets/
│
├── src/
│
└── README.md
```

---

# 📚 Documentation

## Product Documentation

- [Product Vision](docs/PRODUCT_VISION.md)

- [Project Scope](docs/PROJECT_SCOPE.md)

- [Project Decisions](docs/PROJECT_DECISIONS.md)

- [Known Limitations](docs/KNOWN_LIMITATIONS.md)


---

## Functional Requirements

All feature specifications:

```
requirements/
```

Includes:

- CSV Upload
- Validation
- Domain Detection
- Scanning
- Filtering
- Exporting


---

## Technical Documentation

Architecture:

[System Architecture](docs/SYSTEM_ARCHITECTURE.md)


API:

[API Specification](docs/API_SPECIFICATION.md)


Database:

[Database Design](docs/DATABASE_DESIGN.md)


Scanner:

[Scanner Engine](docs/SCANNER_ENGINE.md)


Detection:

[Detection Engine](docs/DETECTION_ENGINE.md)


CSV Processing:

[CSV Processing Engine](docs/CSV_PROCESSING_ENGINE.md)


Testing:

[Testing Strategy](docs/TESTING.md)


Deployment:

[Deployment Guide](docs/DEPLOYMENT.md)


AI Development:

[AI Implementation Rules](docs/AI_IMPLEMENTATION_RULES.md)


---

# ⚙️ Installation

## Requirements

Required:

```
Python 3+

SQLite

Node.js (optional)

Git
```

---

## Clone Repository

```
git clone repository-url
```

Enter project:

```
cd Ads_Detector
```

---

## Install Dependencies

```
pip install -r requirements.txt
```

---

## Setup Database

First run will create:

```
ads_detector.db
```

---

## Start Application

```
python main.py
```

---

# 🖥️ Usage

Basic workflow:

```
1. Upload CSV file

2. Validate domains

3. Start scan

4. Wait for analysis

5. Review results

6. Export leads
```

---

# 📊 Example Use Case

A user uploads:

```
10,000 business domains
```

Ads Detector:

```
Processes domains

↓

Scans websites

↓

Detects advertising tools

↓

Scores prospects

↓

Exports qualified results
```

---

# 🛣️ Roadmap

## Version 1

Completed:

- Documentation
- Architecture planning
- CSV processing design
- Scanner design
- Detection design
- Database planning


---

## Version 2

Planned:

- Full application interface
- Advanced scanning
- More detection rules
- Better filtering


---

## Version 3

Future:

- Cloud version
- Team accounts
- API access
- CRM integration
- AI lead analysis


---

# 🔒 Security

Ads Detector follows:

- Secure file processing
- Browser isolation
- Input validation
- Database protection
- Error logging


---

# 🤝 Contribution

Contributions are welcome.

Before making changes:

1. Read documentation

2. Follow architecture rules

3. Update relevant docs

4. Add tests


---

# 📄 License

This project is licensed under the MIT License.

---

# ⭐ Project Goal

The goal of Ads Detector is to become a complete website intelligence platform that helps users understand the technology landscape behind websites.
