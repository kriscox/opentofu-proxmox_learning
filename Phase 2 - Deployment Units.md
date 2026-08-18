# Phase 2 — Deployment Units

## Purpose

This document contains the working analysis used to identify and define the deployment units of the initial platform scenario.

The resulting deployment units are documented individually under `deployment-units/`.

## Identified Deployment Units

### Vector Agent

**Primary responsibility**

Collect log data from a producing workload and securely forward it to the Log Ingestion and Storage deployment unit.

**Rationale**

The Vector Agent is a reusable deployment unit that can be instantiated alongside multiple producing workloads.

Its baseline configuration is managed centrally, while workload-specific log sources are configured per deployment instance.

### Log Ingestion and Storage

**Primary responsibility**

Receive, process and store log data.

**Included components**

* Vector Server
* Loki

**Rationale**

Vector Server and Loki form a coherent processing and storage capability with a sufficiently aligned lifecycle and operational responsibility to be managed as one deployment unit.

### Observability Visualisation

**Primary responsibility**

Provide access to and visualisation of observability data.

**Included components**

* Grafana

**Rationale**

Grafana has a separate responsibility and lifecycle from log ingestion and storage and can be reused with additional observability data sources.

## Deployment Unit Relationships

The initial architecture follows this dependency chain:

`Producing workload → Vector Agent → Log Ingestion and Storage → Observability Visualisation`

Each deployment unit exposes explicit interfaces and dependencies while remaining independently deployable and manageable as far as reasonably possible.

## Boundary and Responsibility Principles

A functional block and a deployment unit are not the same concept.

* A **functional block** groups components that collectively provide a business or technical capability.
* A **deployment unit** defines a separately deployable and manageable architectural boundary.

Shared capabilities such as network, identity, security and storage remain external dependencies where they do not logically belong inside the deployment unit.

## Current Status

| Subject                       | Status                |
| ----------------------------- | --------------------- |
| Definition of deployment unit | Documented in ADR-001 |
| Vector Agent                  | Defined               |
| Log Ingestion and Storage     | Defined               |
| Observability Visualisation   | Defined               |
| Interfaces and dependencies   | Validated             |
| Deployment-unit model         | Completed             |
