# P5 — Security by design

## Intent

Security must be built into the design, not added afterwards.

## Practice rules

1. **Strong access controls**
   - Strong authentication (MFA mandatory for agents/administrators).
   - SSO (e.g. Entra ID / AD).
   - RBAC with strict separation of duties (least privilege).

2. **Systematic encryption**
   - Encryption in transit (TLS) and at rest.

3. **Compliance and hardening**
   - Follow OWASP guides.
   - Regular security tests (SAST/DAST, code reviews, pentests if needed).
   - Harden Internet-facing interfaces (rate limiting, strict validation, anti-abuse).

4. **Supply chain and dependencies**
   - Dependency scanning, artefact integrity, licence policy.
   - Management of known vulnerabilities (CVE) with prioritization.

5. **“Per-flow” security**
   - Threat modeling by flow type: purchase, permit activation, control, payment, fee/offence issuance, reporting.

## Expected artefacts / evidence

- Documented threat model (at least per “flow” / category).
- Role matrix (RBAC) + effective access controls.
- Security test report (periodic + fixes).
- Secrets management policy (rotation, environment separation).
- List of protections (WAF/anti-abuse/validation) and activation evidence.

## Acceptance criteria

- [ ] MFA and RBAC are active for all sensitive profiles.
- [ ] Critical flows have a maintained and valid threat model.
- [ ] Security scans (code/dependencies) run in the pipeline.
- [ ] Secrets are managed outside code, with rotation and traceability.

## Anti-patterns

- “We’ll add security later”.
- Auth without MFA for at-risk actors.
- Unvalidated interfaces (unconstrained inputs).
- Inconsistent secrets management (no rotation, same keys everywhere).
