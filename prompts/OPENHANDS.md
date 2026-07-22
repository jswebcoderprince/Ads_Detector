# OpenHands Prompt Guide — Ads Detector

## Project Name

Ads Detector

---

# 1. Purpose of This File

This file defines how OpenHands (autonomous coding agent) should operate when working on the Ads Detector repository. It supplements `docs/AI_IMPLEMENTATION_RULES.md`, which remains the primary source of truth for all implementation rules.

---

# 2. Context OpenHands Should Load First

```
docs/SYSTEM_ARCHITECTURE.md

docs/AI_IMPLEMENTATION_RULES.md

docs/CODING_STANDARDS.md

docs/TESTING.md

The relevant requirements/FR-XXX file
```

Because OpenHands operates with autonomous execution capability (running commands, editing multiple files, executing tests), it must load full architectural and testing context before taking any action.

---

# 3. How OpenHands Should Approach a Task

```
Plan the full sequence of steps before executing any file change

Execute changes incrementally, module by module

Run tests after each incremental change

Run linting and formatting before finishing

Report a summary of all files changed
```

OpenHands must not execute a large batch of unrelated file changes in a single autonomous pass; each logical unit of work should be completed and verified before moving to the next.

---

# 4. File and Folder Discipline

- Never create new top-level folders.
- Never rename or delete existing files unless explicitly instructed.
- Never move files between modules without explicit instruction.
- All new files must be placed within the correct existing module directory.

---

# 5. OpenHands-Specific Working Style

- Because OpenHands can execute shell commands, it must only run commands necessary to build, test, lint, or format the project — never destructive or unrelated system commands.
- OpenHands must checkpoint its work frequently (e.g., after each module-level change) so that partial progress can be reviewed or rolled back safely.
- OpenHands must surface any failing test or linting error immediately rather than continuing to build on top of a broken state.

---

# 6. Things OpenHands Must Never Do

```
Modify environment configuration or secrets files without explicit instruction

Delete or overwrite the database file

Disable failing tests instead of fixing the underlying issue

Run commands outside the scope of building, testing, linting, or formatting this project

Push or merge changes without explicit human approval
```

---

# 7. Output Expectations

- Every autonomous change must be accompanied by a clear summary of what was changed and why.
- All code must include type hints, docstrings, and error handling per `docs/CODING_STANDARDS.md` and `docs/ERROR_HANDLING.md`.
- All new functionality must include corresponding tests per `docs/TESTING.md`.

---

# 8. Final Rule

OpenHands' autonomous execution must always remain:

```
Transparent

Incremental

Reversible

Fully tested before completion
```

If at any point a task requires an action outside these bounds, OpenHands should pause and request explicit human confirmation rather than proceeding.
