# Project Agreement

## Purpose

This document captures the working agreements used throughout this project.

Its purpose is to ensure a consistent approach to architecture, documentation, implementation and collaboration. These agreements may evolve during the project as new insights are gained.

---

## Project Principles

- Architecture before implementation.
- Understand before building.
- Work incrementally, one implementation step at a time.
- Each step produces one clear outcome.
- Significant architectural decisions are documented before implementation.
- GitHub is the project's single source of truth.

---

## Learning Approach

The project is used to build both a working platform and architectural understanding.

The preferred learning approach is:

- Explain principles before technology.
- Explain why a decision is made, not only how.
- Introduce one concept at a time.
- Validate understanding before continuing.
- Discuss architectural trade-offs where relevant.
- Keep discussions focused on the current objective.

Each implementation step follows the same structure:

1. Goal
2. Theory
3. One implementation step
4. Verification
5. What we learned

---

## Documentation Principles

- The existing documentation template is the project standard.
- Documentation explains both decisions and their rationale.
- Architectural decisions are recorded as ADRs.
- Documentation evolves together with the implementation.
- Improve the documentation structure only when a real project need has been identified.

---

## Repository Principles

### Shared Repository

The shared repository contains reusable project knowledge, including:

- Architecture
- Design decisions
- Technical documentation
- ADRs
- Infrastructure documentation
- Learning material that is useful to the project

### Private Repository

The private repository contains personal working material, such as:

- Roadmaps
- Planning
- Personal notes
- Draft ideas
- Future topics

---

## Workflow

- Complete one logical step at a time.
- Review before implementation whenever possible.
- Commit related changes together.
- Keep documentation and implementation aligned.
- Update this agreement whenever a new working principle is adopted.

---

## Project Phases

The level of detail depends on the current phase of the project.

### Design

- Focus on architecture and principles.
- Evaluate alternatives and trade-offs.
- Avoid implementation details unless required to support a design decision.

### Implementation

- Execute one implementation step at a time.
- Explain the purpose of each step before performing it.
- Verify the outcome before continuing.

### Troubleshooting

- Identify the root cause before proposing a solution.
- Explain the reasoning process and eliminate possible causes systematically.
- Avoid making assumptions when evidence is missing.

---

## Simplicity and Future Readiness

- Keep personal planning and working documentation as simple as the current need allows.
- Introduce additional structure only when it provides clear value.
- Design the OpenTofu-Proxmox solution for foreseeable growth, maintainability and production use.
- Avoid unnecessary complexity, but do not trade away future extensibility for short-term convenience.
- Prefer architectural choices that can evolve without requiring a complete redesign.