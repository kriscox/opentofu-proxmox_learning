# P1 — Explicit governance of rules and decisions

## Intent

Every decision (business or technical) must be:

- **deterministic** (same inputs => same outputs, for a given rule version),
- **explainable** (understandable by a human),
- **traceable** (linked to a context and a correlation),
- **auditable** (replayable and justifiable).

Related goals: explainability toward the citizen (GDPR art. 22), and ability to reconstruct history via bi-temporality.

## Practice rules

1. **Externalized and versioned rules**  
   - Business rules (rights, pricing, precedence, exceptions, priorities) are stored outside application code, with a version identifier.

2. **Systematic bi-temporality**  
   - Store at least:
     - **business time** (period of applicability),
     - **system time** (moment of recording).
   - Every decision must reference the rule version applied “at the correct business time”.

3. **Decision records (decision evidence)**  
   - For each automated decision, produce a “decision record”:
     - canonical inputs,
     - rules/reference data evaluated (versioned),
     - outputs,
     - bi-temporal timestamps,
     - `correlationId`.

4. **Structured explainability**  
   - The decision returns a `reasonCode` and, when needed, a structured set of “triggered rules”.

5. **Verifiable fairness**  
   - Non-regression tests include multi-zone/municipality cases (bias and behavior-gap checks).

6. **Living documentation**  
   - Documents (reference, decision schemas, rule changelogs) evolve with the rules, not only with the code.

## Expected artefacts / evidence

- Rule catalogue + versioning strategy (e.g. `ruleSetId`, `effectiveFrom`, `effectiveTo`).
- Decision record consultable via audit tools (end-to-end: request => decision => output).
- “Decision replay” test suite (replay a decision identically).
- Rule changelog (who changed what, when, why).

## Acceptance criteria

- [ ] Every automated decision stores a `correlationId`, a `reasonCode`, the rule version, and bi-temporal timestamps.
- [ ] Replaying a historical decision reproduces the same result with the same inputs and the same rule version.
- [ ] Rule priorities (precedence) are explicit, documented, and tested.
- [ ] An auditable rule changelog is available for the current version.

## Anti-patterns

- Rules “hidden” in code without an explicit version.
- Missing bi-temporal references (impossible to reconstruct “what applied then”).
- Decisions that cannot be correlated (no `correlationId`, no input trace).
- Implicit untested priorities (e.g. permit/ticket/exemption overlap).
