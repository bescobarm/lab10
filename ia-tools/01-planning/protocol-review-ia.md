# Review protocol: pre-commit checklist

> **Task reference:** _[Link or ID to the task brief]_  
> **Scope:** Detect AI hallucinations, logic errors, and brief drift before integrating into the repository.

---

## 1. Library and dependency validation

> *Goal: Detect hallucinations (non-existent APIs) and risky or incompatible packages.*

**Key questions**

- Does this `import` / symbol exist in the official documentation for the version you use?
- Is the library maintained, reputable, and compatible with your language/runtime version?
- Is the dependency declared in the project’s dependency file (per the Brief)?

**What to check**

- **Official docs:** Methods, classes, and attributes the AI calls exist in the pinned or intended library version.
- **Environment:** The dependency appears in the manifest lockfile strategy your project uses (`package.json`, `requirements.txt`, `pyproject.toml`, etc.) as agreed in the Brief.
- **Reliability:** Avoid “ghost” or abandoned packages without clear maintenance or adoption.

- [ ] Imports verified against docs or installed artifacts.

---

## 2. Business logic and calculations

> *Goal: Catch domain mistakes, broken rules, and I/O contract mismatches.*

**Key questions**

- Are edge cases handled (empty collections, division by zero, null/undefined/missing fields)?
- Is numeric precision appropriate (e.g. money, rates, aggregates)?
- Do calculations match the behavior described in the Brief?
- Do outputs match the expected schema and types from the Brief?

**What to check**

- **Core logic:** Recheck domain formulas, transformations, and business rules.
- **Data types:** Type safety and precision for sensitive operations (money, IDs, dates).
- **Edge cases:** Boundaries, empty inputs, malformed or oversized payloads.
- **Input/output contract:** Inputs and outputs match the structures described under **Technical requirements** in the Brief.
- **Output validation:** Serialized responses or files match the agreed shape and constraints.
- **Integration points:** External APIs or services are called correctly; responses and errors are handled as specified.

- [ ] Logic and I/O contract verified against the Brief.

---

## 3. Security and input validation

> *Goal: Block vulnerabilities even when the code “works”.*

**Key questions**

- Any hardcoded credentials, API keys, tokens, or secrets?
- Is user or external input validated before domain logic runs?
- Possible injection surfaces (SQL, OS commands, templates, file paths)?
- Least privilege for file, network, and cloud resource access?
- Could logs leak secrets, PII, or auth artifacts?

**What to check**

- **Secret management:** Secrets come from env, secret stores, or project-approved mechanisms—not source.
- **Injection prevention:** No unsafe string concatenation for SQL, shells, or dynamic evaluation.
- **Sanitization:** Paths and user-controlled strings are validated or normalized where needed.
- **Access control:** Permissions are minimal and consistent with the Brief.
- **Logging review:** No sensitive data in log messages or structured log fields.

- [ ] Security and input handling reviewed.

---

## 4. Context and constraint alignment

> *Goal: Ensure the implementation has not drifted from the Brief.*

**Key questions**

- Were all constraints in the Brief respected (architecture, layering, banned patterns)?
- Does the change still target the stated objective without unnecessary scope creep?
- New dependencies: do they violate standards or security rules from the Brief?
- Separation of concerns matches the architecture described in the Brief?
- Are new pieces modular and consistent with project conventions?

**What to check**

- **Dependency guardrails:** No unapproved dependencies vs. **Technical requirements** and **Constraints**.
- **Architectural rules:** Layers/modules match what the Brief specifies.
- **Output format:** Deliverables match **Technical requirements** (output shape, files, APIs).
- **Modularity:** Reuse and boundaries support maintainability.
- **Objective alignment:** Re-read **Context** (problem + goal); confirm the solution addresses that directly.

- [ ] Brief re-read; solution checked point by point.

---

## 5. Stack and quality standards

> *Goal: Match project toolchain, style, and test expectations from the Brief.*

**Key questions**

- Do linting and type-checking (if applicable) pass per project config?
- Do automated tests cover new logic and pass locally/CI?
- Formatting and naming follow repo conventions?
- Leftover `TODO` / `FIXME` that indicate unfinished or risky code?
- Local run succeeds with expected outputs; tests avoid flaky or non-reproducible behavior?

**What to check**

- **Static analysis:** Run configured linters and type checkers; fix or justify any violations allowed by the Brief.
- **Test execution:** Suites green; critical paths and integrations covered as required.
- **Sensitive data:** Logs and test fixtures contain no secrets or unnecessary PII.
- **Code cleanliness:** Remove or ticket any `TODO`/`FIXME` per team policy.
- **Local verification:** Run the app or targeted commands; mock external dependencies in tests for stable, reproducible runs.

- [ ] Quality gates from the Brief and repo are satisfied.

---

## 6. Definition of Done verification

> *Goal: Every DoD item from the Brief is explicitly verified before commit.*

**Key questions**

- Has each DoD checkbox or criterion been met independently?
- Is there observable evidence (test output, artifacts, linter reports, screenshots if UI)?

**What to check**

- [ ] **Objective met:** The concrete goal in **Context** is achieved and demonstrable.
- [ ] **Decoupling:** Domain logic is not unnecessarily tied to infrastructure details (per Brief).
- [ ] **Execution:** The solution runs without errors and produces expected outputs.
- [ ] **Integrations:** Required external systems behave correctly end-to-end where applicable.
- [ ] **Validation:** Automated tests cover core logic and critical integration points.
- [ ] **Quality assurance:** Linting/type-check (if used) clean per project rules.
- [ ] **Delivery:** Source plus updated dependency/config files are consistent and committable.

---

### Final verification

- [ ] Section 1: Libraries and dependencies validated.
- [ ] Section 2: Business logic and I/O contract verified.
- [ ] Section 3: Security and input validation reviewed.
- [ ] Section 4: Brief constraints and architecture alignment confirmed.
- [ ] Section 5: Stack quality standards (linting, tests) passed.
- [ ] Section 6: All DoD criteria from the Brief checked.
- [ ] No disallowed `TODO` / `FIXME` left in code (per team policy).
