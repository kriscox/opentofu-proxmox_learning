# Brief-03 — Decompose the Existing Platform Architecture

## Goal

Analyse the existing platform bootstrap and translate it into the deployment-scope and deployment-unit model.

Use the existing implementation as a source of architectural knowledge, not as a structure that must be copied unchanged.

The objective is to identify coherent lifecycle boundaries, explicit dependencies and unnecessary technical coupling before changing the implementation.

## Source of truth

Use the current default branches of:

* `kriscox/OpenTofu-Proxmox`
* `kriscox/opentofu-proxmox_learning`
* `kriscox/proxmox-bootstrap`

Read the relevant current files before making architectural decisions.

Do not modify or push repository content unless explicitly requested.

## Starting point

The existing `proxmox-bootstrap` implementation already contains responsibilities related to:

* Proxmox host networking;
* VLAN configuration;
* firewall and forwarding;
* storage/snippet configuration;
* bastion infrastructure;
* Kubernetes virtual machines;
* generated configuration and inventory;
* OpenTofu provisioning;
* handover to configuration-management and Kubernetes bootstrap tooling.

These existing implementation boundaries must not automatically become deployment scopes.

## Scope

Analyse each existing platform component and determine whether it is:

* a deployment scope;
* a deployment unit;
* reusable technical implementation;
* scope-specific configuration;
* bootstrap logic;
* or orchestration.

For every candidate deployment scope determine:

* purpose;
* responsibilities;
* lifecycle boundary;
* ownership;
* dependencies;
* provided capabilities;
* consumed capabilities;
* delivery mechanisms currently used;
* state requirements where OpenTofu is used.

## Dependency analysis

Document the existing bootstrap sequence and distinguish:

* real architectural dependencies;
* technical implementation dependencies;
* orchestration order;
* dependencies introduced only by the current tooling.

Identify dependencies that could prevent individual scopes from being deployed or changed independently.

Special attention must be given to the role of Ansible and whether it introduces avoidable bootstrap dependencies.

Do not assume that Ansible must be removed.

The objective is to determine whether infrastructure can be established without requiring an unnecessary external configuration-management dependency.

## Kubernetes distribution

Do not assume K3s or RKE2 in advance.

The existing implementation uses RKE2-related bootstrap patterns.

Evaluate whether:

* RKE2 remains appropriate;
* K3s provides sufficient capability with lower complexity;
* the choice materially affects deployment-scope boundaries or bootstrap dependencies.

The Kubernetes distribution decision must follow from the platform requirements rather than from the learning environment.

## Completion criteria

This brief is complete when:

1. the existing bootstrap architecture has been decomposed;
2. candidate deployment scopes and deployment units are identified and justified;
3. dependencies between scopes are explicit;
4. implementation dependencies are distinguished from architectural dependencies;
5. the role of Ansible is understood;
6. problematic bootstrap coupling is identified;
7. the Kubernetes distribution decision is sufficiently understood to proceed with implementation;
8. the resulting architecture is ready to guide restructuring.
