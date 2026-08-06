# P7 — Observability and traceability

## Intent

Make the system:

- visible,
- measurable,
- and auditable.

## Practice rules

1. **Business and operational monitoring**
   - KPIs, functional alerts (e.g. rights refusal rate, control delays).
   - Technical alerts (SLA/SLO service health).

2. **Centralized and correlatable logs**
   - Centralized logging, correlated with a correlation identifier (`correlationId`).
   - Keep the minimum context needed for audit.

3. **Complete audit**
   - Trace access, actions, and configuration changes.
   - Log “who changed what, when, over which rule period”.

4. **End-to-end tracking**
   - Retrace a decision (inputs => rules => output) as well as an event (control => fee issuance).

## Expected artefacts / evidence

- Correlation and `correlationId` propagation spec.
- Observability architecture (logs/metrics/traces) and retention policies.
- Example of a trace/replay usable in audit.
- Alerting reports (quality, noise, response).

## Acceptance criteria

- [ ] Every critical flow is end-to-end traceable via `correlationId`.
- [ ] Logs/metrics/traces are centralized and consultable in audit.
- [ ] Sensitive actions (access/config changes) are logged.
- [ ] Business and technical alerts are defined with an associated runbook.

## Anti-patterns

- Unstructured logs or logs that cannot be correlated.
- No configuration trace and no rule versioning.
- Observability for “debug only” without business/audit use.
