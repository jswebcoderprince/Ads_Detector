# Codex Prompt Guide — Ads Detector

## Project Name

Ads Detector

---

# 1. Purpose of This File

This file defines how OpenAI Codex-based coding agents should operate when working autonomously or semi-autonomously on the Ads Detector repository. It supplements `docs/AI_IMPLEMENTATION_RULES.md`.

---

# 2. Context Codex Should Load First

```
docs/SYSTEM_ARCHITECTURE.md

docs/AI_IMPLEMENTATION_RULES.md

docs/CODING_STANDARDS.md

The relevant requirements/FR-XXX file

The relevant docs/*_ENGINE.md file for the module being touched
```

---

# 3. How Codex Should Approach a Task

```
Parse the task into the smallest safe unit of change

Locate the exact module the change belongs to

Implement only within that module's boundary

Run linting and formatting before finishing

Run relevant tests before finishing
```

Codex must not restructure unrelated files while completing a task, even if it identifies unrelated issues — unrelated issues should be reported, not silently fixed.

---

# 4. File and Folder Discipline

- Never create new top-level folders.
- Never rename existing files.
- Never move files between modules without an explicit instruction to do so.
- New files must be placed inside the correct existing directory (`csv_processor`, `scanner`, `detection`, `database`, `export`, `core`, `utils`).

---

# 5. Codex-Specific Working Style

- Since Codex often operates with direct file-editing access, every change must be scoped to a single logical unit of work per commit.
- Codex must run the project's formatter and linter (per `docs/CODING_STANDARDS.md`) before considering a task complete.
- Codex must not introduce new dependencies without checking `docs/TECH_STACK.md` first.

---

# 6. Things Codex Must Never Do

```
Modify the database schema without a corresponding migration

Disable or skip failing tests to make a task appear complete

Remove existing error handling or logging

Introduce non-deterministic behavior into detection or scoring logic
```

---

# 7. Output Expectations

- All code changes must include type hints, docstrings, and error handling.
- All new functionality must include at least one corresponding test, per `docs/TESTING.md`.
- All documentation changes must follow the existing structure used in `docs/`.

---

# 8. Final Rule

Codex's autonomous changes must always be:

```
Minimal in scope

Fully tested

Consistent with existing architecture

Reversible
```

If a task cannot be completed without violating one of these principles, Codex should stop and report the conflict rather than proceeding.
