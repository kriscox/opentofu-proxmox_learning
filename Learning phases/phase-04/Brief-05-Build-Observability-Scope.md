# Brief-05 — Build the Observability Scope

## Goal

Implement `ds-observability` on the Kubernetes platform created in Brief-04.

Use Helm as the delivery mechanism for the Kubernetes workloads.

## Starting point

The deployment-unit and deployment-scope boundaries established in Brief-03 remain authoritative.

The expected deployment units are:

### `du-log-ingestion-storage`

* Vector Server;
* Loki.

### `du-observability-visualisation`

* Grafana.

Helm does not define these deployment units. Helm is only the mechanism used to deliver their components.

## Scope

Identify suitable Helm charts for:

* Vector;
* Loki;
* Grafana.

Prefer existing maintained charts over building custom charts.

For each chart:

1. understand its default behaviour;
2. determine which values are required for this platform;
3. avoid changing defaults without a concrete requirement;
4. introduce local configuration only where needed;
5. keep environment-specific differences separate from shared configuration.

## Vector and Loki

Deploy Vector Server and Loki as the implementation of `du-log-ingestion-storage`.

Configure only what is required to:

* receive log data;
* process or forward it as required;
* store it in Loki;
* expose the required Loki interfaces.

## Grafana

Deploy Grafana as `du-observability-visualisation`.

Configure it to consume Loki as a data source.

Keep Grafana lifecycle and configuration separate from the log-ingestion deployment unit.

## Kubernetes integration

Use the capabilities provided by `ds-kubernetes-platform` for:

* Kubernetes runtime;
* ingress;
* persistent storage;
* required network connectivity.

Scope-specific Kubernetes resources, such as the observability namespace, remain owned by `ds-observability`.

## Verification

Verify independently that:

* all Helm releases deploy successfully;
* workloads become healthy;
* persistent volumes are created where required;
* Vector can communicate with Loki;
* Grafana can communicate with Loki;
* required ingress endpoints are reachable.

## Completion criteria

This brief is complete when both observability deployment units are operational on the Kubernetes platform and their configuration is represented reproducibly in the repository.
