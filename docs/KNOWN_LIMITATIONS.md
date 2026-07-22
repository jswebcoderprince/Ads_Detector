# Known Limitations

## Project Name

Ads Detector

---

# 1. Overview

This document describes the current limitations of Ads Detector.

These limitations represent known challenges in the current version and should be considered during development and future improvements.

---

# 2. Detection Accuracy Limitations

## Description

Although Ads Detector uses multiple detection methods, 100% detection accuracy cannot be guaranteed.

Reasons:

- Websites frequently change their scripts
- Tracking systems may use custom implementations
- Some technologies hide their identifiers
- Third-party scripts may be loaded dynamically

---

# 3. JavaScript-Based Detection Limitations

## Description

Some advertising technologies load scripts dynamically after user interaction.

Example:

```
Click event

↓

Tracking script loads
```

In these cases, detection may require advanced browser simulation.

---

# 4. Website Accessibility Limitations

Some websites may not be scanned successfully because of:

- Server downtime
- Firewall protection
- Bot protection
- Geo restrictions
- Slow response time

---

# 5. Anti-Bot Protection

Some websites use:

- Cloudflare protection
- CAPTCHA
- Browser fingerprint detection

These systems may prevent automated scanning.

---

# 6. Dynamic Content Limitation

Modern websites often load content using:

- AJAX
- Single Page Applications
- Client-side rendering

Some technologies may not appear in the initial page load.

---

# 7. New Technology Detection Delay

New advertising platforms may not be detected immediately.

Reason:

Detection requires:

- New patterns
- Updated rules
- New evidence sources

---

# 8. Database Scalability Limitation

SQLite is used for the initial version.

Advantages:

- Simple setup
- Easy deployment

Limitation:

For very large systems:

- Millions of records
- Multiple users
- Heavy concurrent access

A migration to PostgreSQL or another database may be required.

---

# 9. Large Scale Scanning Limitation

Scanning thousands of websites requires significant resources.

Limitations:

- CPU usage
- Memory usage
- Network bandwidth
- Browser instances

Future versions may require:

- Distributed workers
- Cloud infrastructure
- Queue servers

---

# 10. False Positive Possibility

Some detections may occasionally be incorrect.

Example:

A script may contain a similar pattern but not actually represent an advertising technology.

Solution:

- Improve rules
- Increase evidence requirements
- Use confidence scoring

---

# 11. False Negative Possibility

Some technologies may not be detected.

Reasons:

- Custom implementations
- Obfuscated scripts
- Hidden tracking methods

---

# 12. Browser Dependency

The Scanner Engine depends on browser automation.

Possible issues:

- Browser updates
- Compatibility changes
- Resource consumption

---

# 13. No Built-in Lead Qualification

The initial version focuses on technology detection.

It does not automatically determine:

- Business value
- Buying intent
- Revenue potential

Future versions may include AI lead scoring.

---

# 14. Limited Platform Support

Initial detection focuses on major platforms:

```
Google

Meta

TikTok

Microsoft

LinkedIn
```

Additional platforms require new detection rules.

---

# 15. Manual Rule Updates

Detection rules currently require manual updates.

Future improvement:

- AI-generated rules
- Automatic pattern discovery
- Community rule updates

---

# 16. Security Limitations

Although security measures are implemented, website scanning always involves processing external data.

Future improvements:

- Stronger sandboxing
- Cloud isolation
- Advanced threat detection

---

# 17. Future Improvements

Planned improvements:

- Better JavaScript execution analysis
- AI-powered detection
- Cloud scanning infrastructure
- More advertising platforms
- Advanced reporting

---

# 18. Summary

Ads Detector provides valuable website intelligence, but some technical limitations exist due to:

- Website complexity
- Browser restrictions
- Changing technologies
- Large-scale processing challenges

These limitations will be reduced through future development and improvements.
