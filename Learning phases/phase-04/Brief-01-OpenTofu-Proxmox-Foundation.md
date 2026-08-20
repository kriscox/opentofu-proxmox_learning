# Brief 01 — OpenTofu + Proxmox Foundation

We are starting the first hands-on implementation step of Phase 4 of the OpenTofu-Proxmox learning project.

Use the current default branches of these repositories as the source of truth before proposing changes:

- `kriscox/OpenTofu-Proxmox`
- `kriscox/opentofu-proxmox_learning`

Do not rely only on previous conversation context.

## Goal

Teach me the fundamental OpenTofu workflow by deploying one simple virtual machine on Proxmox.

The purpose of this brief is to understand OpenTofu itself before applying the full repository structure, remote state strategy, reusable modules or CI/CD automation.

## Working method

Work with me as a fellow Technical Architect.

Proceed in small, incremental steps and never introduce multiple implementation steps at once.

For each step, focus on:

- Goal
- Theory
- One implementation step
- Verification
- What we learned

Explain why a choice is made, including relevant alternatives and trade-offs.

Do not modify or push repository content unless I explicitly ask. I perform the implementation and pushes myself.

## Scope

Cover only what is required to understand and execute the basic OpenTofu lifecycle:

- confirm the local prerequisites;
- select and understand the Proxmox OpenTofu provider;
- define the authentication approach;
- create the smallest useful OpenTofu configuration;
- deploy one simple Proxmox VM;
- use `tofu init`;
- use `tofu plan`;
- use `tofu apply`;
- inspect the resulting VM and OpenTofu state;
- make one controlled change and inspect the resulting plan;
- remove the VM using OpenTofu.

## Learning focus

Make sure I understand:

- provider;
- resource;
- desired configuration;
- state;
- plan;
- apply;
- destroy;
- how OpenTofu determines change;
- the relationship between configuration, state and actual infrastructure.

## Deliberately out of scope

Do not yet introduce:

- the final deployment-scope repository structure;
- OpenTofu modules unless strictly necessary to explain a concept;
- remote state;
- Azure Blob Storage;
- CI/CD;
- deployment waves;
- cross-scope orchestration;
- production hardening;
- Bicep.

If an important future topic appears, identify it briefly and postpone it.

## Completion criteria

This brief is complete when:

1. OpenTofu can authenticate to Proxmox.
2. One VM has been created through OpenTofu.
3. We have inspected the state and understood its role.
4. One infrastructure change has been planned and applied.
5. The VM has been removed through OpenTofu.
6. I can explain the complete OpenTofu lifecycle in my own words.

At completion, summarize the concrete learning points before moving to Brief 02.
