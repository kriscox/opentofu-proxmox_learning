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

## Cross-scope dependencies and data exchange

Define how independently managed deployment scopes exchange information and how their dependencies are represented technically.

Current direction:

* Each combination of deployment scope and environment has an independent OpenTofu state.
* Dependencies between deployment scopes must remain explicit and should eventually be machine-readable.
* CI/CD orchestration should use these dependencies to determine deployment order.
* A dependency between scopes does not necessarily mean that one scope should directly access the other scope's OpenTofu state.

Options to evaluate for exchanging data between scopes include:

* OpenTofu `terraform_remote_state`;
* explicitly published configuration or outputs;
* provider-specific or platform configuration stores;
* other mechanisms that reduce direct coupling between states.

Architectural concerns:

* Avoid unnecessary coupling between deployment scopes.
* Avoid granting broad access to another scope's state solely to consume a small number of values.
* Consider whether exchanged information may contain sensitive data.
* Keep the dependency direction explicit and understandable.
* Distinguish deployment ordering from data exchange: a scope may depend on another scope being deployed without necessarily consuming its state.

Revisit during:

* OpenTofu implementation design
* Cross-scope dependency design
* Security and access-control design
* CI/CD orchestration design

## State backend requirements

Define the minimum capabilities required from the OpenTofu state backend.

Current requirements:

* State must be stored independently from the machine executing OpenTofu.
* State must be recoverable through versioning, point-in-time recovery or an equivalent mechanism.
* The backend must support state locking to prevent concurrent write operations against the same state.
* Production state must be access-controlled separately from non-production state.
* The backend must support role-based access control with sufficient granularity to introduce additional separation where required.
* State data must be encrypted at rest.
* State data must be encrypted in transit between OpenTofu and the state backend.
* Access to state data must be auditable.
* The backend must provide logs that allow state read, write and delete operations to be traced to an authenticated identity.
* State must be recoverable.
* The backend must provide versioning, point-in-time recovery or an equivalent recovery mechanism.

Topics still to evaluate:

* Access control and separation between environments and deployment scopes.
* Encryption requirements.
* Auditability and logging.
* Availability and disaster-recovery requirements.

Revisit during:

* State backend selection
* Security and access-control design
* CI/CD implementation