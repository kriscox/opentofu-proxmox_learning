# Brief-05 — Build the Kubernetes and Observability Platform

## Goal

Build the Kubernetes platform on top of the infrastructure foundation and deploy the initial observability capability.

The objective is to validate the separation between infrastructure delivery and Kubernetes workload delivery.

## Starting point

The infrastructure scopes from Brief-04 must already provide the capabilities required by the Kubernetes platform.

The Kubernetes distribution selected during Brief-03 is used here.

## Kubernetes platform

Implement the Kubernetes platform using the delivery mechanism established during the architectural analysis.

Determine and implement only what the current use case requires.

This includes, where applicable:

* Kubernetes control plane and workers;
* cluster networking;
* ingress capability;
* persistent storage capability;
* required cluster access;
* required security configuration.

Avoid introducing production-scale HA or additional platform services unless they are required by the current architecture.

## Bootstrap mechanism

Where Kubernetes installation or host configuration currently depends on Ansible, reassess whether that dependency remains justified.

Possible alternatives may include:

* cloud-init;
* installation/bootstrap scripts;
* OpenTofu-triggered guest bootstrap;
* native Kubernetes installation mechanisms.

Do not replace Ansible if the replacement creates a more fragile or opaque solution.

## Observability deployment scope

Implement the observability deployment scope on the Kubernetes platform.

Expected deployment units remain subject to the architecture established in Brief-03.

The current expected model is:

### `du-log-ingestion-storage`

* Vector Server;
* Loki.

### `du-observability-visualisation`

* Grafana.

## Helm

Use Helm as the preferred delivery mechanism for the observability Kubernetes workloads.

Identify maintained Helm charts for:

* Vector;
* Loki;
* Grafana.

Prefer upstream or maintained charts over custom charts.

For each chart:

1. understand the defaults;
2. determine required configuration;
3. override only what the platform requires;
4. keep environment-specific values separate;
5. avoid copying complete upstream charts unless modification is genuinely required.

## Integration

Verify that the observability scope consumes platform capabilities rather than depending on internal Kubernetes-platform implementation details.

Expected capabilities include:

* Kubernetes runtime;
* ingress;
* persistent storage;
* network connectivity.

Scope-owned Kubernetes configuration, such as namespaces and workload-specific resources, remains owned by the observability scope.

## Verification

Verify that:

* Kubernetes becomes operational;
* required storage can be provisioned;
* ingress works;
* Helm deployments succeed;
* Vector can communicate with Loki;
* Loki persists log data as required;
* Grafana can query Loki.

## Completion criteria

This brief is complete when:

1. the Kubernetes platform is operational;
2. observability workloads are deployed reproducibly;
3. platform and workload delivery responsibilities remain separated;
4. any remaining Ansible use is explicit and justified;
5. the observability scope consumes only defined platform capabilities.
