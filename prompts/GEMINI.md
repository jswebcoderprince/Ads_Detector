# Gemini Prompt Guide — Ads Detector

## Project Name

Ads Detector

---

# 1. Purpose of This File

This file defines how Gemini should be used when assisting with the Ads Detector codebase. It supplements `docs/AI_IMPLEMENTATION_RULES.md`, which remains the authoritative source for architecture, security, and coding rules.

---

# 2. Context Gemini Should Load First

```
docs/PRODUCT_VISION.md

docs/SYSTEM_ARCHITECTURE.md

docs/AI_IMPLEMENTATION_RULES.md

The relevant requirements/FR-XXX file
```

---

# 3. How Gemini Should Approach a Task

```
Restate the requirement in its own words before implementing

Identify the correct module boundary

Propose the implementation approach

Implement following existing conventions

Suggest tests and documentation updates
```

---

# 4. File and Folder Discipline

- Do not create new top-level folders.
- Do not rename existing files.
- Keep new code within established module boundaries: `csv_processor`, `scanner`, `detection`, `database`, `export`, `core`, `utils`.

---

# 5. Gemini-Specific Working Style

- Gemini should favor concise, direct implementations over verbose abstractions unless the existing codebase already uses a more abstracted pattern in that module.
- Gemini should explicitly confirm alignment with `docs/PROJECT_SCOPE.md` before implementing any feature that appears to extend beyond documented scope.
- When multiple implementation approaches are viable, Gemini should briefly note the trade-off rather than silently picking one.

---

# 6. Things Gemini Must Never Do

```
Change the database engine or schema without explicit approval

Bypass CSV validation or scanner sandboxing rules

Introduce randomness into confidence scoring

Hardcode secrets or environment-specific values
```

---

# 7. Output Expectations

- Code must include type hints, docstrings, and error handling consistent with `docs/CODING_STANDARDS.md` and `docs/ERROR_HANDLING.md`.
- Documentation must follow the same section structure and level of detail used throughout `docs/`.

---

# 8. Final Rule

Gemini's contributions to Ads Detector must always prioritize:

```
Simplicity

Reliability

Security

Maintainability
```
