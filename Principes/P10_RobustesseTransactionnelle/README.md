# P10 — Transactional robustness

## Intent

Guarantee business consistency despite retries, network latency, and partial failures, especially on critical flows (purchase, control, fees/offence).

## Practice rules

1. **Idempotence by default**
   - Critical write operations require an `idempotencyKey`.
   - Replaying the same request must not create a business duplicate.

2. **Controlled retries**
   - Retry policy with backoff, attempt limits, and handling of permanent vs transient errors.

3. **Explicit business invariants**
   - Examples: no double sale for the same payment intent, no double fee for the same control event in the same window.

4. **Distributed transaction management**
   - Use robust patterns (sagas/compensations) when a global ACID transaction is not possible.

5. **Conflict and concurrency management**
   - Logical locks/optimistic versioning when needed on critical objects (sessions, active permits, control).

6. **State traceability**
   - Every state change is historized with timestamp and correlation.

## Expected artefacts / evidence

- Specification of transactional business invariants.
- Idempotence table/registry and associated retention duration.
- Resilience tests (retries, timeout, message duplication).
- Compensation scenarios documented and tested.

## Acceptance criteria

- [ ] Critical write operations support idempotence (`idempotencyKey`).
- [ ] Business invariants (anti-duplicate, validity windows) are documented and tested.
- [ ] Retry/timeout policies are standardized and verified.
- [ ] Compensations or sagas are defined for distributed workflows.

## Anti-patterns

- Assuming the network is reliable and calls arrive only once.
- Hiding state conflicts without a business signal.
- Building critical workflows without a compensation strategy.
