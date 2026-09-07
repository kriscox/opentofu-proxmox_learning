# Brief-04 — Restructure the Infrastructure Bootstrap

## Goal

Implement the infrastructure-oriented deployment scopes identified in Brief-03.

The objective is to create a reproducible infrastructure foundation while reducing unnecessary bootstrap dependencies.

## Starting point

Use the architectural decomposition from Brief-03 as authoritative.

Reuse useful implementation knowledge from `proxmox-bootstrap`, but do not preserve existing scripts, directory structures or tool choices solely because they already exist.

## Scope

Implement the infrastructure capabilities required before Kubernetes can be installed.

This may include, depending on the boundaries established in Brief-03:

* Proxmox host network configuration;
* VLANs;
* routing and forwarding;
* firewall configuration;
* required storage configuration;
* bastion infrastructure;
* Kubernetes VM infrastructure;
* cloud-init or equivalent guest bootstrap.

## Delivery mechanisms

Use the mechanism that best fits each responsibility.

Possible mechanisms include:

* OpenTofu;
* cloud-init;
* native shell/bootstrap scripts;
* Proxmox-native configuration;
* Ansible where justified.

Do not introduce one tool simply to make all scopes use the same mechanism.

## Ansible dependency review

For every task currently implemented through Ansible, determine:

1. what responsibility the task performs;
2. when it must execute;
3. what it depends on;
4. whether it is required before Kubernetes becomes usable;
5. whether another mechanism can provide the same capability with fewer bootstrap dependencies.

Prefer replacing Ansible where the task naturally belongs in:

* VM creation;
* initial guest configuration;
* cloud-init;
* operating-system bootstrap;
* Kubernetes installation bootstrap.

Keep Ansible where it provides clear value and does not introduce unnecessary lifecycle coupling.

The success criterion is not "zero Ansible".

The success criterion is **no unnecessary dependency on Ansible to establish the infrastructure foundation**.

## OpenTofu

Where OpenTofu is used:

* respect deployment-scope state boundaries;
* keep environment-specific configuration separate;
* create modules only when reuse or encapsulation is demonstrated;
* avoid embedding unrelated lifecycle responsibilities into one state.

## Verification

Verify each infrastructure scope independently where possible.

At minimum confirm:

* network configuration behaves as intended;
* management access remains available;
* required VLAN connectivity works;
* firewall rules enforce the intended boundaries;
* required storage capabilities exist;
* VMs can be created reproducibly;
* VM bootstrap succeeds without hidden manual configuration;
* scopes can be changed without unnecessarily rebuilding unrelated scopes.

## Completion criteria

This brief is complete when:

1. the required infrastructure scopes are implemented;
2. their dependencies are explicit;
3. the infrastructure can be recreated predictably;
4. no unnecessary Ansible dependency exists before Kubernetes bootstrap;
5. remaining configuration-management use is justified;
6. the platform is ready for Kubernetes installation.
