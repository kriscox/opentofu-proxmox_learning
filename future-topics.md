# Topics to remember for later in the next steps

This document captures topics that are intentionally postponed but should be revisited in a later project phase or design step.

## Secrets management strategy

Evaluate a shared secrets management approach for OpenTofu and CI/CD.

Current direction:

* Production: Azure Key Vault is the likely candidate.
* Development/Test on Proxmox: evaluate OpenBao.
* HashiCorp Vault may be compared as an alternative.

Architectural concerns:

* Avoid unnecessary coupling of deployment units to one secrets provider.
* Secrets must not depend on the machine from which OpenTofu is executed.
* Secrets should be centrally available to authorised users and CI/CD pipelines.

Revisit during:

* Environment strategy
* Security hardening

## Deployment and recovery waves

Define a small number of deployment/recovery waves that determine the order in which OpenTofu deployment scopes are restored or deployed.

Current direction:

* **P0 — Landing Zone**

  * Contains only the foundational platform capabilities required for the rest of the environment to operate or be restored.
  * No business applications belong in P0.
  * Typical capabilities may include networking, DNS, firewalling, identity and other foundational platform services.
  * P0 may require a separate or partially manual bootstrap mechanism because the CI/CD platform itself may depend on P0 capabilities.

* **P1–P3**

  * Contain application and platform deployment scopes ordered according to business criticality and recovery needs.
  * Technical dependencies always take precedence over the assigned recovery wave.

The intended recovery flow is:

`P0 → technical validation → P1 → business validation → P2 → validation → P3`

Architectural concerns:

* Recovery wave and technical dependency are different concepts.
* Dependencies determine what must already exist before a deployment scope can run.
* Recovery waves determine business-driven restoration order when multiple scopes are technically ready.
* Recovery wave information should remain visible in the repository rather than existing only inside CI/CD pipelines.
* CI/CD orchestration should later use this information to execute scopes in the required order and introduce validation gates between waves.
* Recovery waves can also provide a useful structure for business acceptance and disaster-recovery testing.

Revisit during:

* CI/CD orchestration design
* Disaster recovery design
* Business validation and recovery testing
