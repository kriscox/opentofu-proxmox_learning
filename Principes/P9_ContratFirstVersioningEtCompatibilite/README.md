# P9 — Contract-first, versioning, and compatibility

## Intent

Integrations must remain stable over time. Any evolution of APIs, events, and schemas must be predictable, testable, and non-destructive for consumers.

## Practice rules

1. **Contract-first**
   - Define contracts (API/event/schema) before implementation.
   - Contracts are versioned and published.

2. **Compatibility strategy**
   - Explicitly define backward/forward compatibility.
   - Any breaking change follows a migration plan and a deprecation schedule.

3. **Systematic versioning**
   - Application version + contract version + schema version.
   - Major/minor/patch changes follow a clear convention.

4. **Schema validation**
   - Strict validation of inbound/outbound payloads.
   - Explicit rejection with readable errors (codes + messages + fields).

5. **Contract tests**
   - Consumer-driven contract tests or equivalent.
   - CI verification to detect integration regressions before delivery.

## Expected artefacts / evidence

- Catalogue of published contracts (APIs/events/schemas).
- Versioning policy + deprecation policy.
- Contract test suite executed in the CI pipeline.
- Contract change log (changelog).

## Acceptance criteria

- [ ] No production contract change is shipped without a version and changelog.
- [ ] Contract tests for critical consumers pass in CI.
- [ ] Compatibility rules (backward/forward) are explicit and applied.
- [ ] Every deprecation has a communicated schedule and migration plan.

## Anti-patterns

- Changing a production contract without a version.
- Coupling consumers to non-contractual internal details.
- Leaving compatibility solely to clients without a migration plan.
