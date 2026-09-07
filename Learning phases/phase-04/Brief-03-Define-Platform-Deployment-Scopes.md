# Brief-03 — Define Platform Deployment Scopes

## Goal

Define the deployment scopes, deployment units and dependencies required for the initial Kubernetes and observability platform.

The objective is to establish the architectural boundaries before implementing infrastructure or workloads.

## Working method

Use the current default branches of these repositories as the source of truth:

* `kriscox/OpenTofu-Proxmox`
* `kriscox/opentofu-proxmox_learning`

Do not implement infrastructure yet.

Work one architectural decision at a time.

Do not create deployment units or scopes merely to fit a repository structure. Each boundary must have a clear responsibility and lifecycle justification.

Do not modify or push repository content unless explicitly requested.

## Scope

Define at least these deployment scopes:

### `ds-kubernetes-platform`

A platform capability providing the Kubernetes environment required by dependent deployment scopes.

Determine:

* purpose;
* responsibilities;
* scope boundaries;
* dependencies;
* provided capabilities;
* deployment units, if any are justified;
* lifecycle boundary;
* selected delivery mechanisms.

The initial platform is expected to provide the capabilities required by the observability use case, including:

* Kubernetes cluster access;
* ingress capability;
* persistent storage capability;
* required network connectivity.

### `ds-observability`

A platform capability providing central log ingestion, storage and visualisation.

The initial composition is expected to contain:

* `du-log-ingestion-storage`

  * Vector Server;
  * Loki.
* `du-observability-visualisation`

  * Grafana.

Validate these boundaries against the current architectural definitions rather than accepting them automatically.

## Dependencies

Define the dependency between:

```text
ds-observability
        ↓ depends on
ds-kubernetes-platform
```

Describe the dependency in terms of capabilities rather than internal implementation.

## Completion criteria

This brief is complete when:

1. both deployment scopes have clear responsibilities and boundaries;
2. their deployment units are identified and justified;
3. dependencies between the scopes are explicit;
4. required capabilities provided by `ds-kubernetes-platform` are documented;
5. delivery mechanisms are identified without making them part of the architectural definition;
6. the resulting architecture is ready for implementation.
