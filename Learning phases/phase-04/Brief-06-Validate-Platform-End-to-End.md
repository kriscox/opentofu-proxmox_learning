# Brief-06 — Validate the Platform End to End

## Goal

Validate the complete chain from infrastructure provisioning to observable log data.

The purpose is to prove that the architecture, dependencies and delivery mechanisms work together as intended.

## Scope

Test the complete deployment chain:

```text
Proxmox
   ↓
ds-kubernetes-platform
   ↓
K3s
   ↓
ds-observability
   ├── Vector Server
   ├── Loki
   └── Grafana
```

## Test sequence

### Platform validation

Verify that the Kubernetes platform provides:

* a working cluster;
* ingress;
* persistent storage;
* required connectivity.

### Observability validation

Verify that:

* Vector Server accepts test log data;
* the log data reaches Loki;
* Loki stores the data;
* Grafana can query Loki;
* the test log can be found through Grafana.

### Dependency validation

Verify that deployment order matters as expected.

`ds-observability` must rely only on the explicitly defined capabilities of `ds-kubernetes-platform`.

Identify any hidden dependency discovered during testing.

### Lifecycle validation

Validate the lifecycle of both scopes.

At minimum:

* deploy;
* verify;
* make a controlled configuration change;
* verify the change;
* remove the deployment where appropriate;
* recreate it;
* verify that the resulting platform remains predictable.

### Architecture validation

After the technical tests, review whether implementation revealed problems in:

* deployment-scope boundaries;
* deployment-unit boundaries;
* dependencies;
* delivery-mechanism selection;
* repository structure;
* state boundaries.

Architectural documentation should only be changed where the implementation provides concrete evidence that an earlier assumption was incorrect.

## Completion criteria

This brief is complete when:

1. the Kubernetes platform can be deployed reproducibly;
2. the observability scope can be deployed on top of it;
3. a test log travels successfully through Vector and Loki to Grafana;
4. persistence and ingress behave as expected;
5. dependencies between the scopes are confirmed;
6. lifecycle operations are predictable;
7. architecture and implementation are consistent.
