# P2 — Sovereignty and control of data, code, and hosting

## Intent

The organization retains full control of its digital assets:

- **data**,
- **code**,
- **infrastructure / hosting**.

## Practice rules

1. **Single source of truth per entity**
   - For each business entity (plate, zone, session, ticket, sale, permit, grids, control, offence), define which database / service is “authoritative”.

2. **Data lifecycle and governance**
   - Minimization, pseudonymization where possible, and retention policies.
   - Explicitly handle export and deletion in line with GDPR.

3. **GDPR + NIS2 compliance**
   - Define operational security, traceability, and incident-management requirements.

4. **Code ownership and reversibility**
   - Contracts/licences that enable continuity (escrow/IP if needed).
   - Ability to extract, migrate, or delete code and data.

5. **Traced software supply chain**
   - Dependency inventory (SBOM),
   - OSS licence compliance,
   - vulnerability tracking (CVE) and acceptance policy.

6. **Hosting located in European territory**
   - Choose the EU, ideally Belgium where possible, with contractual guarantees.

## Expected artefacts / evidence

- “Entity -> source of truth” matrix.
- Retention/export/deletion policies.
- SBOM + licence compliance report (per version).
- Security dossier: secrets inventory, rotation, and hosting documentation.
- Reversibility plan (process + responsibilities).

## Acceptance criteria

- [ ] Every business entity has a single documented and validated source of truth.
- [ ] GDPR policies (retention, export, deletion) are applied and testable.
- [ ] An SBOM and a licences/CVE report are produced at each release.
- [ ] A reversibility plan provides the steps to export/migrate code and data.

## Anti-patterns

- Several undocumented “sources of truth”.
- Uninventoried dependencies (or no SBOM/licence strategy).
- No documented GDPR export/deletion process.
- Business logic coupled to a vendor (non-standard data/IDs, proprietary schemas).
