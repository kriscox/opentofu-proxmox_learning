# Phase 2 — Deployment Units

## Purpose

This document contains the working analysis used to identify and define the deployment units of the platform.

It supports the Phase 2 architecture work and remains personal working documentation until the proposed deployment units, their boundaries and their dependencies are sufficiently stable to be documented in the shared platform repository.

## Current architectural context

The initial learning scenario contains a log aggregation block with the following components:

* Vector Agent
* Vector Server
* Loki
* Grafana

The block describes a functionally coherent solution, but it is not automatically one deployment unit.

A deployment unit is a separately deployable and manageable architectural unit with its own responsibility, lifecycle, boundaries, security considerations and explicit dependencies.

## Current working proposal

The log aggregation block currently contains two identified deployment units.

### Log Ingestion and Storage

**Primary responsibility**

Receive, process and store log data.

**Included components**

* Vector Server
* Loki

**Current rationale**

Vector Server and Loki form a closely connected processing and storage chain. They are expected to share a sufficiently related lifecycle and operational responsibility to be treated as one deployment unit.

**External dependencies**

* Kubernetes runtime
* Persistent storage
* Network connectivity
* Central routing and firewall enforcement
* Log producers, including Vector Agents

The deployment unit must describe the network flows it requires. The central network or security capability remains responsible for implementing routing and firewall rules at the boundaries it owns.

### Observability Visualisation

**Primary responsibility**

Provide access to and visualisation of observability data.

**Included components**

* Grafana

**Current rationale**

Grafana has a separate responsibility and can evolve independently from the log ingestion and storage capability.

It may later be reused for additional observability data sources, such as metrics or traces. This gives it a different lifecycle and reuse potential from Vector Server and Loki.

**External dependencies**

* Kubernetes runtime
* Loki as an initial data source
* Network connectivity
* Identity and access capabilities when user access is introduced

## Boundary and responsibility notes

A functional block and a deployment unit are not the same concept.

* A **functional block** groups components that collectively provide a business or technical capability.
* A **deployment unit** defines a separately deployable and manageable architectural boundary.

One functional block may therefore contain multiple deployment units.

A deployment unit does not necessarily own every external configuration it requires.

For example:

* The log-related deployment unit defines the communication flows it requires.
* The central network or security capability implements and manages routing and firewall rules at the boundaries it owns.
* Both responsibilities and the resulting dependency must be documented explicitly.

## Open questions

* Is the Vector Agent a reusable deployment unit or part of each producing workload?
* Are Vector Server and Loki sufficiently aligned in lifecycle and responsibility to remain one deployment unit?
* Which central capability owns VLAN creation, routing and firewall enforcement?
* How should required changes in other deployment units be declared and validated?
* Which security controls belong inside each deployment unit and which are external dependencies?

## Current status

| Subject                         | Status                            |
| ------------------------------- | --------------------------------- |
| Definition of deployment unit   | Documented in ADR-001             |
| Log Ingestion and Storage       | Initial candidate                 |
| Observability Visualisation     | Initial candidate                 |
| Vector Agent boundary           | To be analysed                    |
| Network and firewall dependency | Identified, not yet fully defined |
| Complete deployment-unit model  | In progress                       |
