# Phase 3 — OpenTofu Foundation

## Key learnings

### 1. Architecture boundaries and OpenTofu management boundaries are different concepts

Deployment units describe architectural capabilities and responsibilities.

A functional capability managed through OpenTofu may nevertheless require several deployment units to work together.

This led to the additional concept of a deployment scope.

**What I learned:** an architectural building block does not automatically need its own OpenTofu state or deployment lifecycle.

### 2. Deployment unit, deployment scope and OpenTofu module should not be forced to align

The three concepts solve different problems:

* a deployment unit defines an architectural responsibility;
* a deployment scope defines an OpenTofu composition and management boundary;
* an OpenTofu module defines a reusable technical implementation capability.

A deployment scope can use several deployment units and modules, while a module can be reused by several scopes.

**What I learned:** forcing architecture, state and implementation abstractions into identical boundaries creates coupling rather than simplicity.

### 3. State boundaries should follow management and failure boundaries

Each deployment scope is instantiated independently for each environment.

This means that a deployment scope in TST, UAT and PRD has separate state, and unrelated deployment scopes within the same environment also have separate state.

**What I learned:** state is not merely a technical file. Its boundary determines what OpenTofu manages together and therefore influences locking, blast radius, lifecycle and recovery.

### 4. OpenTofu state is management data, not a runtime dependency

The state backend is required when OpenTofu manages or changes infrastructure.

Already deployed infrastructure normally continues to operate when the state backend is temporarily unavailable.

**What I learned:** availability requirements for management-plane components should be derived from their actual operational role rather than automatically copied from production workload requirements.

### 5. State recovery and infrastructure rollback are different operations

Recovering a previous state version is intended to repair damaged or lost management information.

Normal infrastructure rollback should happen by restoring the intended configuration and applying that configuration again.

**What I learned:** source-controlled configuration describes the intended infrastructure; state records OpenTofu's management knowledge about that infrastructure. They are related but not interchangeable.

### 6. A remote state backend does not need to run where the managed infrastructure runs

Azure Blob Storage can hold OpenTofu state even when OpenTofu manages local Proxmox infrastructure.

The execution environment only needs secure connectivity and appropriate authentication to the backend.

**What I learned:** the location of the state backend and the location of the managed resources are independent architectural decisions.

### 7. Portability does not mean avoiding provider-specific capabilities

Azure Blob Storage was preferred because it fits the organisation's existing platform and identity ecosystem.

At the same time, the design retains alternatives and ensures that migration to another supported backend remains realistic.

The same reasoning applies to OpenTofu modules: provider-specific modules are acceptable when a generic abstraction would add unnecessary complexity.

**What I learned:** reducing lock-in means understanding dependencies and preserving reversibility, not refusing every provider-specific capability.

### 8. Repository boundaries are not architectural boundaries

Deployment units, deployment scopes and modules can initially coexist in one repository.

They can later move to separate repositories if ownership, lifecycle or scale justifies it without changing their architectural meaning.

**What I learned:** repository structure is an implementation and collaboration choice. Architecture should remain valid even if source-code organisation changes.

### 9. Environment differences should extend a shared definition rather than duplicate it

A deployment scope represents the same capability across TST, UAT and PRD.

Environment-specific configuration should contain only the differences required for that environment.

**What I learned:** modelling environments as variations of one shared definition reduces drift and keeps architectural intent consistent.

### 10. Deployment order should be explicit information, not encoded in names

Numeric prefixes can make an initial repository look ordered, but deployment and recovery order can change independently from the identity of a component.

Dependencies and future recovery waves should therefore be represented as metadata or orchestration information.

**What I learned:** identity and ordering are different concerns. Encoding operational behaviour into names makes future changes harder.

## Overall takeaway

The most important Phase 3 insight is that **architecture, deployment composition, state, reusable modules, environments and repositories are separate dimensions**. They interact, but they should only share boundaries when there is a concrete reason. Keeping those concerns separate creates a platform that can evolve without forcing architectural redesign whenever an implementation choice changes.
