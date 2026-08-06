# P3 — Independence and portability

## Intent

The architecture must remain agnostic to vendors and technologies, and allow recovery without depending on a single actor.

## Practice rules

1. **Reversibility via open standards**
   - Data models, protocols, and formats must be accessible and documented.

2. **Dependency encapsulation**
   - Every vendor dependency is identified, documented, and encapsulated (ports/adapters).

3. **Legacy / new component coexistence**
   - Older logics (meters, proxies, historical systems) may coexist with newer modules.

4. **Transferable operational documentation**
   - Ensure skills continuity: procedures, runbooks, operating models.

5. **BCP/DRP (continuity plan)**
   - Covers: vendor disappearance, major incident, key-team unavailability.

## Expected artefacts / evidence

- Dependency map (tech + vendor) + isolation plan.
- Stable identifier/schema conventions (contracts).
- Operating runbooks + skills-transfer guides.
- BCP/DRP plan tested or at least scenario-walked.

## Acceptance criteria

- [ ] Critical vendor dependencies are inventoried with an encapsulation strategy.
- [ ] A vendor-exit scenario is documented and executable.
- [ ] Operating and recovery runbooks exist and are up to date.
- [ ] The BCP/DRP plan is tested or, at minimum, simulated with a report.

## Anti-patterns

- Hidden vendor lock-in (tools embedded in business “core”).
- Proprietary formats that cannot be replaced without a redesign.
- No runbook / no recovery simulation.
