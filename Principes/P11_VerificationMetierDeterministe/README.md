# P11 — Deterministic business verification

## Intent

Prove over time that business decisions remain correct, explainable, and stable for a given rule version.

## Practice rules

1. **Golden datasets**
   - Maintain representative case suites (zones, municipalities, exceptions, edge cases, geographic boundaries).
   - Each case contains input, temporal context, and expected output.

2. **Decision non-regression tests**
   - Run tests on every evolution of rules, schemas, or evaluation code.
   - Systematically compare expected vs actual.

3. **Historical replay**
   - Ability to replay past decisions with the rule versions of that time.
   - Bi-temporal verification (business time vs system time).

4. **Minimum business coverage**
   - Define functional coverage goals (nominal cases, errors, legally sensitive cases).

5. **Gap governance**
   - Every gap between expected and actual is analyzed and traced to a decision (fix, migration, justified exception).

## Expected artefacts / evidence

- Versioned business test-case reference.
- Non-regression report per release.
- Replay / audit journal of historical decisions.
- Coverage table for critical business scenarios.

## Acceptance criteria

- [ ] A versioned golden dataset exists for each critical rule family.
- [ ] Business non-regression tests run on every release.
- [ ] Historical decision replay is possible and verifiable in audit.
- [ ] Every expected/actual divergence is traced, analyzed, and adjudicated.

## Anti-patterns

- Validating rules only by hand, without an automated suite.
- Changing rules without updating reference cases.
- Not distinguishing application bugs from intentional functional evolution.
