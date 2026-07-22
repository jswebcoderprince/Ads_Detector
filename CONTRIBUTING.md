# Contributing Guide

**Project:** Ads Detector Documentation

**Version:** 1.0

**Status:** Active

---

# Purpose

This document defines the standards and workflow for contributing to the Ads Detector project documentation and source code.

The goal is to ensure consistency, maintainability, and high-quality implementation across all future development.

---

# Project Philosophy

Every contribution should make the project:

- Easier to maintain
- Easier to understand
- More reliable
- More scalable
- Better documented

Do not add unnecessary complexity.

Keep every solution simple, readable, and modular.

---

# Development Principles

All contributors should follow these principles:

- Keep functions small and focused.
- Write reusable code.
- Prefer readability over cleverness.
- Avoid unnecessary dependencies.
- Follow the existing folder structure.
- Document important decisions.
- Keep business logic separate from UI.

---

# Documentation Standards

Every documentation file should:

- Have a clear title.
- Explain its purpose.
- Be written in Markdown.
- Use consistent formatting.
- Include examples where appropriate.
- Avoid ambiguous language.

Documentation should be understandable by both developers and AI coding assistants.

---

# Coding Standards

### Backend

- Python 3.12+
- FastAPI
- Type hints required
- Modular architecture
- One responsibility per module

### Frontend

- React
- Vite
- Tailwind CSS
- Functional components only
- Reusable UI components

### Browser Automation

- Playwright
- Chromium
- Headless mode by default

---

# Git Workflow

Recommended workflow:

1. Create a new branch.
2. Make one logical change.
3. Test the change.
4. Update documentation if needed.
5. Commit with a meaningful message.
6. Merge after review.

Example commit messages:

```
feat: add Google Ads detector

fix: improve CSV parser

docs: update API specification

refactor: simplify scanner engine
```

---

# Folder Structure

Do not create new folders unless necessary.

Follow the existing project structure.

Keep related files together.

---

# Naming Conventions

### Markdown Files

Use uppercase with underscores.

Example:

```
PROJECT_SCOPE.md
SYSTEM_ARCHITECTURE.md
```

Requirement documents:

```
FR-001_UPLOAD_CSV.md
FR-008_DETECT_GOOGLE_ADS.md
```

### Python Files

Use lowercase with underscores.

Example:

```
scanner_engine.py
csv_parser.py
browser_manager.py
```

### React Components

Use PascalCase.

Example:

```
UploadCard.jsx
ProgressBar.jsx
ResultsTable.jsx
```

---

# Pull Request Checklist

Before submitting changes, verify:

- Code builds successfully.
- Documentation is updated.
- No unnecessary files are added.
- Folder structure remains clean.
- Naming conventions are followed.
- Existing functionality is not broken.

---

# Documentation Update Policy

Whenever functionality changes:

- Update the relevant Functional Requirement.
- Update API documentation if applicable.
- Update Architecture documentation if affected.
- Update README when necessary.

Documentation should always reflect the current implementation.

---

# AI Development Guidelines

When using AI coding assistants:

- Read the documentation before writing code.
- Do not invent new features.
- Follow the documented architecture.
- Keep implementation aligned with the Functional Requirements.
- Ask for clarification instead of making assumptions.

---

# Quality Standards

A contribution is considered complete only if it:

- Meets the documented requirements.
- Passes testing.
- Includes documentation updates.
- Maintains consistent code style.
- Does not introduce unnecessary complexity.

---

# Version Control

Every major documentation change should include:

- Version number
- Date
- Summary of changes

---

# Final Rule

The documentation is the single source of truth.

If the implementation and documentation differ, the documentation must be updated immediately or the implementation must be corrected.
