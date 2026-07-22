# FR-017: Application Settings

## Requirement ID

FR-017

---

## Requirement Name

Application Configuration and User Settings Management

---

# Purpose

The Application Settings module allows users to configure Ads Detector according to their workflow and system capability.

The purpose of this module is to provide flexibility while maintaining safe default configurations.

---

# Related User Stories

- US-022: Configure Application
- US-023: Customize Scan Behavior
- US-024: Manage Application Preferences

---

# Functional Description

The system shall provide a settings panel where users can modify application behavior.

Settings should be stored locally and automatically loaded when the application starts.

---

# Settings Workflow

```
Open Application

↓

Load Saved Settings

↓

Apply Configuration

↓

Run Application

↓

Save Updated Changes
```

---

# Settings Categories

The settings module should contain:

```
Scanner Settings

Detection Settings

Export Settings

Database Settings

Interface Settings
```

---

# 1. Scanner Settings

## Purpose

Controls website scanning behavior.

---

## Scan Timeout

Defines maximum waiting time for a website.

Default:

```
30 seconds
```

User options:

```
10 seconds

30 seconds

60 seconds

120 seconds
```

---

## Concurrent Scans

Controls how many websites can be scanned simultaneously.

Default:

```
5 websites
```

Options:

```
1

3

5

10
```

---

## Browser Mode

Options:

```
Headless Mode

Visible Browser Mode
```

---

## JavaScript Execution

Option:

```
Enable JavaScript

Disable JavaScript
```

Default:

```
Enabled
```

---

## Cookie Collection

Option:

```
Collect Cookies

Disable Cookie Collection
```

---

# 2. Detection Settings

## Purpose

Controls advertising technology detection behavior.

---

## Confidence Threshold

Minimum confidence score required.

Default:

```
50
```

Example:

```
Show only results above 50%
```

---

## Enable Detectors

Users can enable or disable:

```
Google Ads

Meta Pixel

TikTok Pixel

Microsoft UET

LinkedIn Insight

Pinterest Tag
```

---

## Auto Detection Updates

Future option:

```
Enable automatic detector updates
```

---

# 3. Export Settings

## Purpose

Controls exported file behavior.

---

## Default Export Format

Options:

```
CSV

Excel

JSON
```

Default:

```
CSV
```

---

## Export Columns

Users can choose:

```
Domain

Ads Platform

Confidence

Score

Tags

Notes

Evidence
```

---

## Export Location

Default:

```
User Documents Folder
```

---

# 4. Database Settings

## Purpose

Manage local data storage.

---

## Database Location

Display:

```
ads_detector.db
```

---

## Backup Database

Option:

```
Create Backup
```

Output:

```
ads_detector_backup.db
```

---

## Restore Database

Option:

```
Restore Backup
```

---

## Clear Database

Danger action:

```
Delete All Data
```

Confirmation required.

---

# 5. Interface Settings

## Theme

Options:

```
Light

Dark

System Default
```

---

## Table Display

Options:

```
Rows Per Page:

25

50

100
```

---

## Notifications

Options:

```
Enable Notifications

Disable Notifications
```

---

# Settings Storage

Settings should be stored locally.

Database table:

```
settings
```

---

Fields:

```
id

setting_name

setting_value

updated_at
```

---

# Default Configuration

First application launch:

System should create:

```
Default Settings
```

Example:

```
Timeout:

30 seconds


Concurrency:

5


Export:

CSV
```

---

# Reset Settings

Users should have:

```
Reset To Default
```

option.

---

# Validation Rules

The system should prevent invalid values.

Example:

Invalid:

```
Concurrency = -5
```

Result:

```
Invalid value.
Please select a valid number.
```

---

# Performance Requirements

Settings changes should apply immediately where possible.

Example:

Changing:

```
Rows per page
```

should update instantly.

---

# Error Handling

## Settings Save Failed

Message:

```
Unable to save settings.
```

---

## Invalid Configuration

Message:

```
Invalid configuration detected.
Default values restored.
```

---

# Acceptance Criteria

The feature is complete when:

## AC-001

Users can access settings panel.

---

## AC-002

Scanner settings can be modified.

---

## AC-003

Export preferences can be changed.

---

## AC-004

Settings remain after application restart.

---

## AC-005

Users can restore default settings.

---

## AC-006

Database backup options are available.

---

# Future Improvements

Possible enhancements:

- Cloud settings sync
- User profiles
- Advanced proxy settings
- Multiple scanner profiles
- Team configurations

---

# Summary

FR-017 gives users control over how Ads Detector operates.

By providing configurable settings, the application can work efficiently on different machines and adapt to different scanning requirements.

The goal is:

```
Simple Default Setup

+

Advanced User Control
```
