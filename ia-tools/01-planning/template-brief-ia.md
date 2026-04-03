# AI brief — Master template

> Copy this file, rename it for the task, and fill in every section. This is not a specific task: it is a reusable mold for delegating complex work to the AI with less ambiguity.

---

## Task title

<!-- Short, actionable name (e.g. "Add CSV export to the reports module"). -->

**Title:** _[fill in]_

---

## Context

The AI needs to understand the problem before proposing code or solutions. Without this block it tends to produce generic or incorrect answers.

### Current system or environment

- _[What exists today: repo, services, relevant code areas, runtime environment.]_

### Problem to solve

- _[What fails, what is missing, or what friction exists today.]_

### Concrete goal for this task

- _[What must be resolved when the brief is closed, in one or two measurable sentences.]_

---

## Technical requirements

They define **how** the solution must be implemented and reduce the chance the AI picks an approach incompatible with your stack.

| Area | Detail |
|------|--------|
| Language / runtime | _[e.g. Python 3.12, Node 20, etc.]_ |
| Patterns / architecture | _[layers, hexagonal, feature folders, etc.]_ |
| Expected input | _[format, source, basic validation.]_ |
| Expected output | _[format, contracts, error codes.]_ |
| Integrations | _[APIs, queues, DB, SDKs; links or names of existing modules.]_ |
| Files / modules touched | _[paths or names if you already know them.]_ |

_Additional notes:_

- _[Any naming conventions, error handling, or logging rules to follow.]_

---

## Constraints

What the AI must **not** do and the standards it **must** follow.

- _[e.g. type hints required, no new dependencies, stdlib only, etc.]_
- _[e.g. comply with repo ESLint/Ruff/black.]_
- _[e.g. automated tests required for changes in X.]_
- _[e.g. do not change public contracts without notice / migration.]_

---

## Definition of Done

**Verifiable** criteria to consider the task done (a measurable goal, not a vague “when it works”).

- [ ] _[Tests: which suite or cases must pass.]_
- [ ] _[Performance: latency, size, limits if applicable.]_
- [ ] _[Functional: behavior you can verify step by step.]_
- [ ] _[Output format: response shape, generated files, etc.]_
- [ ] _[Human review: short checklist or PR ready to merge per team rules.]_

---

# Review protocol (post-AI, pre-commit)

Fixed checklist to catch common issues in AI-generated code **before** you commit. Customize the last item for your stack.

## 1. Real APIs and libraries (hallucinations)

**Key question:** Do that import and that API actually exist?

**What to check:**

- Official package documentation.
- Package repository (releases, maintenance).
- Compatibility with your language version and OS/environment.

- [ ] Imports verified against docs or installed code.

## 2. Business logic

**Key question:** Do calculations and rules match the domain?

**What to check:**

- Critical formulas (money and decimals, percentages, accumulations).
- Boundary conditions and edge cases.
- Appropriate numeric types (avoid floats for money when inappropriate).

- [ ] Formulas and rules reviewed with boundary cases.

## 3. Security

**Key question:** Is the code secure even if it “works”?

**What to check:**

- Injection (SQL, templates, commands).
- Input validation and sanitization.
- Credentials and secrets (not in repo, not in logs).
- Authentication/authorization and data exposure.

- [ ] Attack surface and sensitive data reviewed.

## 4. Alignment with the brief (lost context)

**Key question:** Were **all** constraints and requirements met?

**What to check:**

- Allowed dependencies vs. those used.
- Agreed input/output structure.
- Project rules (style, layers, conventions).

- [ ] Brief re-read; solution checked point by point.

## 5. Custom item (your stack)

**Key question:** _[Define your own environment-specific question.]_

**Focus examples:**

- New tests run in local CI / pipeline.
- Logs without PII or secrets.
- Internal architecture compliance (bounded contexts, forbidden modules, etc.).

**Your checklist:**

- [ ] _[Fill in with your project-specific criterion.]_

---

## Quick start

1. Duplicate this file → `brief-<short-name>.md`.
2. Fill in **Title**, **Context**, **Requirements**, **Constraints**, and **DoD**.
3. After the AI responds, run through the **Review protocol** before commit.
