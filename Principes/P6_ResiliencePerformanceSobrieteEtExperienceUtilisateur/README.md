# P6 — Resilience, performance, sobriety, and user experience

## Intent

The system must be:

- available,
- performant,
- accessible,
- and sober in resource usage.

## Practice rules

1. **Availability and fault tolerance**
   - High availability, graceful degradation.
   - Fallback strategies and management of dependency on external services.

2. **Scalability**
   - Horizontal scalability and peak control (especially “purchase” and “control” flows).

3. **Digital sobriety**
   - Right-sizing.
   - Shut down non-prod environments outside hours.
   - Eco-design (limit useless processing, pagination, reasoned caching).

4. **Measurable objectives**
   - Define SLO/SLI (latency, error rate, availability) by flow type.

5. **Interfaces and UX**
   - Preference for “thin client” web interfaces.
   - Native multilingual support (FR/NL minimum, EN if required).
   - Accessibility (WCAG) + backward compatibility.

## Expected artefacts / evidence

- Versioned SLO/SLI + observability dashboards.
- Capacity plans and load tests.
- Sobriety indicators (consumption/cost/carbon per your model).
- Accessibility compliance (WCAG check) for key screens.

## Acceptance criteria

- [ ] SLO/SLI for critical flows are defined, measured, and monitored.
- [ ] Load tests prove peak-traffic handling.
- [ ] Graceful-degradation mechanisms are documented and tested.
- [ ] UX requirements (WCAG, multilingual) are validated on critical journeys.

## Anti-patterns

- Optimizing only the average without addressing p95/p99.
- Leaving dependencies without latency budgets.
- Designing inaccessible UX (WCAG) or untested multilingual flows.
