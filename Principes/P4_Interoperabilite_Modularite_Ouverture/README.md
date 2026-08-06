# P4 — Interoperability, modularity, and openness

## Intent

Exchanges must go through reliable and evolvable integration mechanisms.

The system must be designed to:

- evolve,
- open to the ecosystem,
- support multi-tenancy (multi-municipality, multi-zone, multi-regulation).

## Practice rules

1. **Normalization of formats & identifiers**
   - Normalize: schemas, protocols, IDs, time semantics (UTC vs business time).
   - Version APIs/events and manage compatibility.
   - **Integration reference standard**: [APDS](https://allianceforparkingdatastandards.org/) for the services core (see [ADR-001](../../decisions/ADR-001-alignement-apds.md)).

2. **Native multi-tenancy**
   - The "tenant" (municipality/zone/district/operator scope) is part of the data model and execution context.

3. **Decoupled business modules**
   - Separate responsibilities: rights, pricing, sessions, sales, control, fees/revenue, reporting.

4. **Interoperability with legacy**
   - Via an abstraction layer: proxies, adapters, gateways.
   - **Explicit mapping** between existing APIs and the internal APDS model (anti-corruption layer).

5. **Open data / transparency**
   - Meet obligations: provide public data when required.

6. **Integration APIs**
   - Enable integration: mobility apps, GPS, citizens (simulators), integrators.

## Expected artefacts / evidence

- API catalogue (public/private) + versioning policy.
- Identifier conventions (tenant/zone/district IDs).
- Compatibility strategy (backward/forward) + contract tests.
- Interoperable schemas and integration documentation.

## Acceptance criteria

- [ ] API/event contracts are documented, versioned, and accessible.
- [ ] Tenant context (municipality/zone/district) is present in flows that require it.
- [ ] Contract tests pass for critical integrations.
- [ ] Business modules evolve without strong coupling to a channel or vendor.
- [ ] V1-scope APDS alignment is documented; legacy mappings are identified.

## Anti-patterns

- Centralizing all business logic on the integration side without decoupling.
- Forcing every municipality to "fork" the application code.
- Modeling national/municipal concepts without "tenant context".
