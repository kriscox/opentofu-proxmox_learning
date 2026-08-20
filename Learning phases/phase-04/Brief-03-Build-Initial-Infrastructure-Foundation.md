# Brief 03 — Build the Initial Infrastructure Foundation

We are continuing Phase 4 of the OpenTofu-Proxmox learning project after:

1. learning the basic OpenTofu + Proxmox lifecycle;
2. validating the Phase 3 OpenTofu structure on a real deployment scope.

Use the current default branches of these repositories as the source of truth before every significant design step:

- `kriscox/OpenTofu-Proxmox`
- `kriscox/opentofu-proxmox_learning`

## Goal

Build the initial Proxmox infrastructure foundation using the validated OpenTofu architecture and repository structure.

The purpose is no longer to learn isolated OpenTofu commands, but to start constructing the real infrastructure model that later platform services and CI/CD will use.

## Working method

Work with me as a fellow Technical Architect.

Do not design the entire infrastructure in one pass.

Proceed deployment scope by deployment scope and dependency by dependency.

Before implementing a new scope:

1. establish its responsibility and boundary;
2. identify dependencies;
3. decide whether existing deployment units and modules are sufficient;
4. determine the correct state boundary;
5. implement only that scope;
6. verify it before moving on.

Challenge unnecessary abstractions, coupling and premature modules.

Do not modify or push repository content unless I explicitly ask.

## Scope

Build the infrastructure foundation required for the later platform services.

This may include, based on the actual architecture and Proxmox environment:

- foundational Proxmox VM infrastructure;
- network-related infrastructure;
- storage-related requirements;
- reusable VM provisioning capabilities;
- multiple deployment scopes;
- explicit deployment-scope dependencies;
- environment-specific configuration;
- OpenTofu modules where reuse or encapsulation is demonstrated;
- remote state for each deployment scope and environment.

The exact infrastructure components must be derived from the current architecture and repository content rather than assumed in advance.

## Architectural focus

For every new component, explicitly consider:

- Is this a deployment unit, deployment scope, OpenTofu module, or simply configuration?
- What is its lifecycle?
- Who owns it?
- What depends on it?
- What state should manage it?
- Could a failure or change affect unrelated scopes?
- Is reuse real or hypothetical?
- Does the implementation introduce provider lock-in, and is that acceptable?
- What will CI/CD later need to know about this dependency?

## Deliberately out of scope

Do not yet implement the full CI/CD solution.

CI/CD-related needs may be recorded as requirements, but automation belongs to the later CI/CD phase.

Also keep Bicep out of scope.

## Completion criteria

This brief is complete when:

1. the initial Proxmox infrastructure foundation has been represented through deployment scopes;
2. dependencies between those scopes are explicit;
3. each scope has a clear OpenTofu state boundary;
4. reusable technical capabilities have modules only where justified;
5. the infrastructure can be created, changed and removed predictably through OpenTofu;
6. the resulting structure is ready to host the platform services from the next project phase.

At completion, perform an architecture review before starting Phase 5.
