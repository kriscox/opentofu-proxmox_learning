# Brief-06 — Validate Independent Deployment and Recovery

## Goal

Validate the complete platform architecture, deployment dependencies and lifecycle behaviour.

The objective is not only to prove that the platform works, but that the deployment-scope model supports predictable creation, change, recovery and replacement.

## Scope

Validate the complete chain derived from the final architecture.

Conceptually:

```text
Proxmox host
    ↓
Infrastructure foundation
    ↓
VM infrastructure
    ↓
Kubernetes platform
    ↓
Observability
```

The actual scope names and boundaries must follow the architecture established in Brief-03.

## Functional validation

Verify that:

* infrastructure scopes deploy correctly;
* Kubernetes becomes usable;
* observability workloads become healthy;
* Vector receives test log data;
* log data reaches Loki;
* Loki stores it;
* Grafana can query and display it.

## Dependency validation

For each deployment scope:

* confirm its declared dependencies;
* identify any hidden dependencies;
* distinguish deployment order from architectural coupling;
* verify that unrelated scopes do not need to be redeployed.

Pay particular attention to dependencies on:

* Ansible;
* generated local files;
* manual host configuration;
* shared state;
* implicit script execution order.

## Lifecycle validation

Where safe and appropriate, test:

* initial deployment;
* repeated deployment;
* controlled configuration change;
* independent scope change;
* destruction and recreation;
* recovery after partial failure.

Verify that rebuilding one scope does not unnecessarily affect unrelated scopes.

## Bootstrap validation

Perform or simulate a clean bootstrap from an empty infrastructure starting point.

Document every external prerequisite required before automation can begin.

The desired result is a bootstrap chain without hidden circular dependencies.

Where manual bootstrap remains necessary, confirm that it is:

* minimal;
* explicit;
* documented;
* stable;
* intentionally outside automated lifecycle management.

## Architecture review

Review whether implementation revealed problems in:

* deployment-scope boundaries;
* deployment-unit boundaries;
* state boundaries;
* delivery-mechanism selection;
* dependency metadata;
* repository structure;
* bootstrap responsibilities.

Do not change architectural decisions merely to match the existing implementation.

Change them only where implementation demonstrates that the architectural model is incorrect or impractical.

## Completion criteria

This brief is complete when:

1. the platform can be built from its defined starting conditions;
2. dependencies between deployment scopes are explicit;
3. no hidden bootstrap dependency remains;
4. infrastructure and Kubernetes workloads can evolve with appropriate lifecycle independence;
5. observability works end to end;
6. remaining Ansible use is understood and justified;
7. rebuild and recovery behaviour is predictable;
8. architecture and implementation are consistent.
