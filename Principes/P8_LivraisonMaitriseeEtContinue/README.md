# P8 — Controlled and continuous delivery

## Intent

The delivery cycle must be automated, secured, and controlled.

## Practice rules

1. **Strictly separated environments**
   - dev, test, staging, production.

2. **Controlled promotion**
   - Human validation at key steps (e.g. release candidate, schema changes, sensitive rules).

3. **Business non-regression tests**
   - “Golden” decision scenarios for rules/rights/tariffs before production.

4. **DevSecOps**
   - Infrastructure as code, secured pipelines.
   - Centralized configuration management (rules, grids, policies).

5. **Simulation and real-condition testing**
   - Flow simulation (purchase, control, fee issuance).
   - Legacy/equipment integration verification when relevant.

6. **Automatic dependency verification**
   - Licence compliance and dependency integrity on every build.

## Expected artefacts / evidence

- Documented (and auditable) CI/CD pipeline.
- List of human gatekeepers + pass criteria.
- Business decision test suite (versioned by rules).
- SBOM evidence + vulnerability scans (CVE) per build/release.
- Deployment/rollback runbooks.

## Acceptance criteria

- [ ] Dev/test/staging/prod environments are unambiguously separated.
- [ ] The pipeline includes security and business non-regression gates.
- [ ] Promotions to production require human validation at critical steps.
- [ ] A rollback plan is defined and tested.

## Anti-patterns

- Deploying without business tests.
- Mixing dev/staging/prod to “go faster”.
- Changing schema or rules without a bi-temporal strategy / migration plan.
