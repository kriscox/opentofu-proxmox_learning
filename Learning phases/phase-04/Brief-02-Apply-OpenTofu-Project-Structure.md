# Brief 02 — Apply the OpenTofu Project Structure

We are continuing Phase 4 of the OpenTofu-Proxmox learning project after completing the basic OpenTofu + Proxmox lifecycle from Brief 01.

Use the current default branches of these repositories as the source of truth before proposing changes:

- `kriscox/OpenTofu-Proxmox`
- `kriscox/opentofu-proxmox_learning`

Read the relevant Phase 3 ADRs, OpenTofu standards and templates before proposing the implementation structure.

## Goal

Take the simple Proxmox deployment from Brief 01 and restructure it according to the architectural and OpenTofu conventions defined in Phase 3.

This is the point where we validate whether our Phase 3 design actually works in practice.

## Working method

Work with me as a fellow Technical Architect.

Proceed one design or implementation decision at a time.

Explain:

- why the structure is needed;
- what problem it solves;
- whether the Phase 3 rule is still appropriate after practical use;
- what should be changed if implementation evidence contradicts the earlier design.

Do not preserve an earlier decision merely because it already exists in an ADR.

Do not modify or push repository content unless I explicitly ask.

## Scope

Use the existing Phase 3 decisions to introduce the practical structure for one real deployment scope.

Work through, where applicable:

- deployment-scope directory structure;
- `README.md`;
- `metadata.yaml`;
- `opentofu/`;
- `variables.tf`;
- `outputs.tf`;
- `environments/<environment>.tfvars`;
- naming and coding standards;
- environment-specific overrides;
- state boundary per deployment scope and environment;
- remote state using the selected state-backend strategy;
- OpenTofu modules only when the implementation demonstrates real reuse or encapsulation value.

## Validation focus

Explicitly test the important Phase 3 assumptions:

- Can one shared OpenTofu implementation serve multiple environments?
- Are environment-specific files limited to overrides?
- Are shared defaults in the right place?
- Does the deployment-scope lifecycle remain coherent?
- Is the state boundary practical?
- Does the repository structure remain understandable?
- Are inputs and outputs sufficient without exposing internals?
- Does a shared change allow impact analysis across all environments?

If an architectural decision proves impractical, stop and discuss the design before continuing.

## Deliberately out of scope

Do not yet build the full platform.

Also postpone:

- CI/CD automation;
- recovery waves;
- broad cross-scope orchestration;
- production hardening;
- Bicep.

## Completion criteria

This brief is complete when:

1. One real deployment scope follows the agreed repository structure.
2. Environment-specific configuration is working.
3. Remote state is working according to the selected strategy.
4. The relevant coding standards have been applied.
5. We have decided whether an OpenTofu module is justified for the implementation.
6. The Phase 3 architecture has been practically validated and any required corrections have been documented.

At completion, summarize which Phase 3 decisions were confirmed, changed or deferred before moving to Brief 03.
