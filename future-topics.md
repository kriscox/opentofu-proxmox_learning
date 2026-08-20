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

Topics still to evaluate:

* Access control and separation between environments and deployment scopes.
* Encryption requirements.
* Auditability and logging.
* Availability and disaster-recovery requirements.

Revisit during:

* State backend selection
* Security and access-control design
* CI/CD implementation

## Verification-only CI/CD execution

Provide a CI/CD execution mode that validates the intended infrastructure change without applying it.

Current direction:

* Validation and planning must be usable independently from deployment.
* A pipeline should be able to determine the expected infrastructure changes before an apply operation is authorised.
* Verification-only execution should support review, impact assessment and controlled production changes.

Architectural concerns:

* Validation must not unintentionally modify managed infrastructure.
* The result should provide sufficient information for technical review and approval.
* The same configuration and state boundaries should be used for verification and deployment.
* Verification-only execution may later support drift detection, but drift-management behaviour should be designed separately.

Revisit during:

* CI/CD pipeline design
* Change and approval workflow design
* Drift-management design

## OpenTofu and Kubernetes deployment responsibilities

Define the boundary between infrastructure provisioning with OpenTofu and deployment of Kubernetes platform components and workloads.

Current direction:

* OpenTofu provisions and configures infrastructure required by the platform.
* OpenTofu may also manage Kubernetes and Helm resources where this provides a coherent, reproducible deployment flow.
* Helm remains the packaging and deployment mechanism for Kubernetes applications and platform components where appropriate.
* Infrastructure provisioning and Kubernetes workload deployment do not necessarily need to share the same lifecycle or CI/CD flow.

Architectural concerns:

* Avoid coupling application lifecycle unnecessarily to infrastructure lifecycle.
* Keep ownership boundaries between infrastructure, platform and application deployments explicit.
* Do not use OpenTofu modules merely to hide Helm or Kubernetes implementation details without a meaningful abstraction.
* Determine where OpenTofu responsibility should end and application-specific deployment tooling should begin.

Revisit during:

* OpenTofu implementation design
* Kubernetes platform design
* CI/CD orchestration design
* Application deployment strategy

## Bastion and administrative access architecture

Evaluate whether a bastion host, jump host or equivalent controlled administrative access capability is required.

Current direction:

* Do not introduce a bastion solely because it is common in reference architectures.
* Introduce an additional administrative access layer only when concrete security, network or operational requirements justify it.

Architectural concerns:

* Administrative access should follow least-privilege and auditable access principles.
* Additional infrastructure introduces operational responsibilities and another security-sensitive component.
* Cloud-native or identity-aware access mechanisms may remove the need for a traditional bastion.

Revisit during:

* Network and security architecture
* Administrative access design
* Production security hardening

## Local Kubernetes development environment

Validate how OpenTofu interacts with a local Kubernetes environment used for learning and development.

Current question:

* Determine whether and how OpenTofu should target a local Kubernetes runtime such as Rancher Desktop during development and testing.

Architectural concerns:

* The local development mechanism must not become an implicit production architecture dependency.
* Configuration should remain sufficiently portable to validate the same concepts against the intended platform environments.
* Environment-specific implementation differences should remain explicit.

Revisit during:

* First OpenTofu implementation
* Environment strategy
* Kubernetes development workflow
