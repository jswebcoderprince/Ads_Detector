# ChatGPT Prompt Guide — Ads Detector

## Project Name

Ads Detector

---

# 1. Purpose of This File

This file defines how ChatGPT should be used when assisting with the Ads Detector codebase. It supplements `docs/AI_IMPLEMENTATION_RULES.md`, which remains the authoritative source for architecture, security, and coding rules.

---

# 2. Context ChatGPT Should Load First

Before answering any implementation question, provide ChatGPT with:

```
docs/PRODUCT_VISION.md

docs/PROJECT_SCOPE.md

docs/SYSTEM_ARCHITECTURE.md

docs/AI_IMPLEMENTATION_RULES.md

The relevant requirements/FR-XXX file
```

ChatGPT should not be asked to implement a feature without first being given the relevant FR document and architecture context.

---

# 3. How ChatGPT Should Approach a Task

```
Read the requirement

Identify the correct module

Propose an implementation plan before writing code

Write code matching existing conventions

Suggest tests

Suggest documentation updates
```

---

# 4. File and Folder Discipline

- Do not suggest new top-level folders.
- Do not suggest renaming existing files.
- Keep new code within the established module boundaries: `csv_processor`, `scanner`, `detection`, `database`, `export`, `core`, `utils`.

---

# 5. ChatGPT-Specific Working Style

- When asked broad questions, ChatGPT should first summarize its understanding of the requirement before producing code, to catch misunderstandings early.
- ChatGPT should avoid proposing third-party libraries not already listed in `docs/TECH_STACK.md` unless explicitly asked to evaluate alternatives.
- ChatGPT should flag any requirement that appears to conflict with `docs/PROJECT_SCOPE.md` rather than silently expanding scope.

---

# 6. Things ChatGPT Must Never Do

```
Invent new architecture patterns not documented in SYSTEM_ARCHITECTURE.md

Bypass the CSV validation or scanner sandboxing rules

Suggest storing secrets in code

Change confidence scoring logic without flagging the change explicitly
```

---

# 7. Output Expectations

When ChatGPT produces code:

- Include type hints, docstrings, and error handling consistent with `docs/CODING_STANDARDS.md` and `docs/ERROR_HANDLING.md`.

When ChatGPT produces documentation:

- Match the section structure and level of detail already used in `docs/`.

---

# 8. Final Rule

Every ChatGPT-assisted contribution to Ads Detector must prioritize:

```
Simplicity

Reliability

Security

Maintainability
```
