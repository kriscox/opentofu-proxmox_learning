# Brief-04 — Build the Kubernetes Platform

## Goal

Implement the initial `ds-kubernetes-platform` on Proxmox.

The result must be a small but usable Kubernetes platform capable of hosting the observability scope.

## Starting point

The architecture and boundaries defined in Brief-03 are authoritative for this implementation.

Do not expand the platform beyond requirements demonstrated by the initial observability use case.

## Scope

Build an initial Kubernetes environment based on:

* one Proxmox virtual machine;
* K3s;
* required network configuration;
* required firewall configuration;
* ingress capability;
* persistent storage capability.

Use OpenTofu where infrastructure provisioning is appropriate.

Additional configuration mechanisms may be used where OpenTofu is not the appropriate tool, but their role must remain explicit.

## Implementation principles

### Proxmox VM

Provision the VM reproducibly.

At minimum, determine and implement:

* CPU;
* memory;
* storage;
* network configuration;
* operating system requirements.

Avoid premature abstraction.

Create an OpenTofu module only when reuse or encapsulation is demonstrated.

### K3s

Install and configure K3s on the VM.

The implementation must result in a usable Kubernetes API and cluster.

Do not introduce multi-node or high-availability design unless required by the current use case.

### Ingress

Provide an ingress capability sufficient for workloads deployed in the next brief.

Use the capabilities already available through K3s where they satisfy the requirement unless there is a concrete architectural reason to replace them.

### Storage

Provide persistent storage suitable for the initial observability workloads.

The implementation only needs to satisfy the current platform requirements.

Do not introduce a production-scale storage architecture prematurely.

### Network and firewall

Allow only the connectivity required to:

* administer the platform;
* access the Kubernetes API where required;
* expose required ingress endpoints;
* support the observability workloads.

## Verification

Verify independently that:

* the VM can be created reproducibly;
* K3s starts correctly;
* Kubernetes API access works;
* ingress capability is available;
* persistent storage can be provisioned;
* required network connectivity works;
* infrastructure can be removed predictably.

## Completion criteria

This brief is complete when `ds-kubernetes-platform` provides a working Kubernetes environment with the capabilities required by `ds-observability`.
