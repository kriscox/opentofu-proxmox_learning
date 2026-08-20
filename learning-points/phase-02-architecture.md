# Phase 2 — Architecture

## Key learnings

### 1. A functional capability is not automatically one deployment unit

A functional capability may consist of several components with different responsibilities, lifecycles or ownership.

Grouping everything that belongs functionally together can create unnecessarily large deployment and responsibility boundaries.

**What I learned:** deployment-unit boundaries should be based primarily on responsibility, lifecycle, ownership and manageable coupling rather than only on functional grouping.

### 2. A deployment unit needs one coherent responsibility

A deployment unit should represent a capability that can be understood, deployed, secured and managed as one coherent architectural boundary.

For the observability scenario this resulted in separate responsibilities for log collection, log ingestion and storage, and visualisation.

**What I learned:** component boundaries become much clearer when I first ask *what is this unit responsible for?* rather than *which products belong together?*

### 3. Reusability can reveal architectural boundaries

The Vector Agent initially appeared closely related to the log ingestion platform because both use Vector.

However, the agent is deployed alongside producing workloads and can be reused independently for many producers.

**What I learned:** products do not determine architectural boundaries. The same technology can belong to different deployment units when it performs different responsibilities or follows a different lifecycle.

### 4. Shared capabilities should remain explicit dependencies

Capabilities such as networking, identity, security and storage do not automatically belong inside every deployment unit that uses them.

They should remain external when they have their own responsibility and are shared across the platform.

**What I learned:** dependencies are not a weakness in architecture. Hidden or poorly defined dependencies are. Explicit dependencies allow boundaries to remain clean without pretending components are independent when they are not.

### 5. Architecture boundaries should be enforceable where practical

A boundary should not exist only in a diagram.

Infrastructure, network, runtime, storage, identity and security controls can help enforce the separation between deployment units.

**What I learned:** a useful architecture boundary should eventually correspond to something observable or enforceable in the implemented platform, although perfect technical isolation is not always necessary.

### 6. Avoid introducing components without a concrete requirement

During the architecture discussion, components such as a bastion host could easily have been added because they commonly appear in reference architectures.

We deliberately postponed such components until an actual access or security requirement justifies them.

**What I learned:** reference architectures are sources of patterns, not checklists. Architecture should solve known requirements rather than reproduce a standard diagram.

## Overall takeaway

Good architecture decomposition is primarily about responsibilities and lifecycles, not products or diagrams. Clear boundaries, explicit dependencies and conscious reuse make it possible to evolve individual capabilities without unnecessarily coupling the complete platform.
