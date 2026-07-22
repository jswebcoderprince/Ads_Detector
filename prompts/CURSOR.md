# Cursor Prompt Guide — Ads Detector

## Project Name

Ads Detector

---

# 1. Purpose of This File

This file defines how Cursor's in-editor AI assistance should be used when working on the Ads Detector codebase. It supplements `docs/AI_IMPLEMENTATION_RULES.md`.

---

# 2. Context Cursor Should Load First

```
docs/SYSTEM_ARCHITECTURE.md

docs/AI_IMPLEMENTATION_RULES.md

docs/CODING_STANDARDS.md

The file(s) currently open in the editor

Any FR-XXX file referenced in the current task
```

Cursor should rely on the open editor context plus the above documentation rather than assuming project structure from memory.

---

# 3. How Cursor Should Approach a Task

```
Read surrounding code in the currently open file

Match existing patterns in that file and its module

Avoid introducing a different style within the same file

Suggest, not force, larger refactors
```

---

# 4. File and Folder Discipline

- Do not use Cursor's multi-file edit capability to create new top-level folders.
- Do not rename files as part of an unrelated inline suggestion.
- Keep generated code within the module the currently open file belongs to.

---

# 5. Cursor-Specific Working Style

- Since Cursor operates inline within the editor, suggestions should be scoped tightly to the function or file currently being edited.
- Cursor should avoid proposing sweeping changes across multiple modules in a single suggestion; large changes should be broken into smaller, reviewable edits.
- Autocomplete-style suggestions must still include type hints and docstrings consistent with `docs/CODING_STANDARDS.md`.

---

# 6. Things Cursor Must Never Do

```
Auto-apply changes to the database schema

Auto-apply changes to security-sensitive code (validation, sandboxing) without explicit review

Suggest removing existing tests

Suggest hardcoded configuration values
```

---

# 7. Output Expectations

- Inline suggestions must match the formatting and linting conventions already present in the file being edited.
- Any suggestion touching detection rules or confidence scoring must be flagged for manual review before acceptance.

---

# 8. Final Rule

Cursor-assisted edits must remain:

```
Small in scope

Consistent with surrounding code

Reviewed before acceptance for security-sensitive modules
```
