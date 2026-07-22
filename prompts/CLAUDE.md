# Claude Prompt Guide — Ads Detector

## Project Name

Ads Detector

---

# 1. Purpose of This File

This file tells Claude how to work on the Ads Detector codebase. It supplements `docs/AI_IMPLEMENTATION_RULES.md`, which remains the primary source of truth for all implementation rules. Use this file for Claude-specific working conventions only.

---

# 2. Context Claude Should Load First

Before making any change, Claude should read, in this order:

```
docs/PRODUCT_VISION.md

docs/PROJECT_SCOPE.md

docs/SYSTEM_ARCHITECTURE.md

docs/AI_IMPLEMENTATION_RULES.md

The specific FR-XXX file in requirements/ related to the task
```

Do not skip `AI_IMPLEMENTATION_RULES.md` — it defines the non-negotiable architecture, security, and naming rules for this project.

---

# 3. How Claude Should Approach a Task

```
Understand the requirement

Check existing modules for related logic

Reuse before creating new files

Implement in the correct module boundary

Add tests

Update documentation
```

Never implement a feature by guessing scope. If a requirement is ambiguous, check the corresponding `requirements/FR-XXX_*.md` file first.

---

# 4. File and Folder Discipline

- Do not create new top-level folders.
- Do not rename existing files or folders.
- Place new code inside the correct existing module (`csv_processor`, `scanner`, `detection`, `database`, `export`, `core`, `utils`).
- New documentation must follow the structure and tone already used in `docs/`.

---

# 5. Claude-Specific Working Style

- Prefer small, reviewable changes over large rewrites.
- When editing a file, preserve unrelated code and formatting exactly as-is.
- When writing Markdown documentation, follow the same section order used across the project's existing `docs/` files.
- When uncertain about a technology decision, check `docs/PROJECT_DECISIONS.md` before proposing an alternative.

---

# 6. Things Claude Must Never Do

```
Introduce a new database engine without explicit approval

Bypass the modular architecture

Skip error handling or logging

Hardcode secrets or configuration values

Silently change existing detection scoring logic
```

---

# 7. Output Expectations

When Claude produces code:

- Include type hints and docstrings, per `docs/CODING_STANDARDS.md`.
- Include error handling, per `docs/ERROR_HANDLING.md`.

When Claude produces documentation:

- Match the existing Markdown style used elsewhere in the repository.
- Keep explanations detailed and production-level, not brief summaries.

---

# 8. Final Rule

Claude's implementations must always prioritize:

```
Simplicity

Reliability

Security

Maintainability
```

Every change must move Ads Detector closer to its documented product vision without introducing instability.
