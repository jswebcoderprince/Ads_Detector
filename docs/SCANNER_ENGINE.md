# Scanner Engine

## Project Name

Ads Detector

---

# 1. Overview

The Scanner Engine is the core component responsible for visiting websites and collecting technical information required for advertising technology detection.

The scanner analyzes websites by loading pages in a controlled browser environment and collecting:

- HTML content
- JavaScript files
- Network requests
- Cookies
- Tracking scripts
- Third-party resources

The collected information is passed to the Detection Engine for analysis.

---

# 2. Scanner Engine Responsibilities

The Scanner Engine is responsible for:

- Opening websites
- Managing browser sessions
- Capturing website resources
- Monitoring network activity
- Handling failed scans
- Managing scan timeouts
- Sending collected data to Detection Engine

---

# 3. Scanner Architecture

```
Scan Queue

      |

      ↓

Scanner Manager

      |

      ↓

Browser Controller

      |

      ↓

Website Session

      |

      ↓

Data Collector

      |

      ↓

Detection Engine
```

---

# 4. Scanning Workflow

```
Domain Received

↓

Create Scan Task

↓

Launch Secure Browser

↓

Load Website

↓

Capture Data

↓

Close Browser

↓

Send Data For Detection

↓

Save Results
```

---

# 5. Browser Automation Layer

The scanner uses browser automation to simulate a real user visit.

Supported technologies:

```
Playwright

Puppeteer

Selenium
```

Recommended:

```
Playwright
```

because it provides:

- Better browser control
- Network monitoring
- Modern JavaScript support
- Reliable automation

---

# 6. Browser Isolation

Every scan should run inside an isolated browser environment.

Requirements:

- New browser context
- No saved cookies
- No personal data
- No browser extensions
- No user sessions

Example:

```
Scan Website A

↓

Temporary Browser Session

↓

Destroy Session
```

---

# 7. Website Loading Process

When scanning a website:

Steps:

```
Open URL

↓

Wait For Page Load

↓

Execute JavaScript

↓

Monitor Requests

↓

Collect Evidence
```

---

# 8. Data Collection

The scanner collects:

## HTML Data

Examples:

```
Page source

Meta information

Script tags
```

---

## JavaScript Resources

Examples:

```
tracking.js

pixel scripts

analytics files
```

---

## Network Requests

The scanner monitors:

```
GET requests

POST requests

Third-party connections
```

---

## Cookies

Collected information:

```
Cookie names

Cookie domains

Cookie providers
```

---

# 9. Network Monitoring

The scanner tracks external connections.

Example:

Website:

```
example.com
```

Request:

```
connect.facebook.net
```

Detection:

```
Meta Pixel
```

---

# 10. JavaScript Detection Support

The scanner analyzes JavaScript files for patterns.

Example:

```
gtag()

fbq()

ttq()
```

Possible detection:

```
Google Ads

Meta Pixel

TikTok Pixel
```

---

# 11. Scan Queue Integration

The Scanner Engine receives tasks from:

```
Scan Queue Manager
```

Queue states:

```
Pending

Processing

Completed

Failed
```

---

Example:

Input:

```
1000 websites
```

Queue:

```
website-1 Processing

website-2 Pending

website-3 Pending
```

---

# 12. Timeout Management

Every website scan must have a maximum execution time.

Default:

```
30 seconds
```

If timeout occurs:

```
Save Error

Continue Next Website
```

---

# 13. Error Handling

Possible errors:

## Website Not Available

Example:

```
DNS Error
```

Action:

```
Mark Failed
Continue Scan
```

---

## SSL Error

Example:

```
Certificate Invalid
```

Action:

```
Record Warning
Continue
```

---

## Server Timeout

Action:

```
Retry Once

Then Mark Failed
```

---

# 14. Retry System

Failed websites may retry.

Default:

```
Maximum Retries: 2
```

Example:

```
Attempt 1 Failed

↓

Retry

↓

Attempt 2 Failed

↓

Save Failure
```

---

# 15. Resource Control

The scanner should control:

## CPU Usage

Prevent overload.

---

## Memory Usage

Limit browser sessions.

---

## Concurrent Browsers

Default:

```
5 Workers
```

---

# 16. Scanner Output

The Scanner Engine produces:

```
HTML Data

Scripts

Network Logs

Cookies

Resources
```

Example:

```json
{
 "domain":"example.com",
 "scripts":[
   "gtag.js"
 ],
 "requests":[
   "google.com"
 ]
}
```

---

# 17. Security Rules

The scanner must:

- Block dangerous downloads
- Prevent file execution
- Use isolated sessions
- Limit permissions

---

# 18. Performance Optimization

Techniques:

- Parallel scanning
- Request filtering
- Cache control
- Worker management

---

# 19. Future Improvements

Possible upgrades:

- Distributed scanners
- Cloud browsers
- Proxy rotation
- Geographic scanning
- Mobile device simulation

---

# 20. Summary

The Scanner Engine is responsible for collecting raw website intelligence.

Complete flow:

```
Domain

↓

Secure Browser

↓

Website Analysis

↓

Evidence Collection

↓

Detection Engine

↓

Final Result
```

The Scanner Engine provides the foundation for accurate advertising technology detection.
