# Assets Directory

## Overview

This directory contains static, non-code assets used across the Ads Detector project and its documentation, including icons, images, and screenshots. It is organized into three subfolders to keep asset types clearly separated.

## Purpose

The purpose of this directory is to:

- Provide a single, predictable location for all visual assets referenced by the README, documentation, and application interface.
- Keep binary/visual assets separate from source code and Markdown documentation.
- Ensure assets referenced in documentation remain organized and easy to locate as the project grows.

## Detailed Explanation

### Subfolders

- `icons/` — small iconography used in the application interface or documentation (e.g., status icons, technology category icons).
- `images/` — general-purpose images used in documentation or marketing material (e.g., diagrams exported as images, illustrative graphics).
- `screenshots/` — screenshots of the application's Dashboard, Filtering System, and other UI screens, used to illustrate functionality in the README and documentation.

## Functional Requirements

- Any image referenced in `README.md` or files under `docs/` must be stored in the appropriate subfolder here, not committed elsewhere in the repository.
- File names within each subfolder must be descriptive (e.g., `dashboard_filtered_view.png`) rather than generic (e.g., `screenshot1.png`).

## Technical Considerations

- Image files should be reasonably compressed before being committed, to avoid unnecessarily bloating the repository size.
- Preferred formats are `.png` for screenshots and UI captures, and `.svg` where possible for icons, to preserve scalability.

## Workflow / Process

```
New Visual Asset Created
              ↓
Correct Subfolder Identified (icons / images / screenshots)
              ↓
File Named Descriptively
              ↓
Referenced from README.md or Relevant docs/ File
              ↓
Committed Alongside the Change That Introduced It
```

## Error Handling

- Broken image references in documentation must be treated as a documentation defect and corrected as soon as identified.

## Security Considerations

- Screenshots must not include real user data, real domain names belonging to third parties, or any sensitive configuration values; use sanitized or placeholder data when capturing screenshots.

## Future Improvements

- Add a naming convention document if the number of assets grows large enough to require stricter organization.
- Consider adding an automated check that flags unused assets no longer referenced by any documentation file.

## Summary

The `assets/` directory centralizes all visual, non-code resources used by Ads Detector's documentation and interface, organized into `icons/`, `images/`, and `screenshots/` subfolders for clarity and easy maintenance.
