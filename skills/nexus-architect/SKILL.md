---
name: nexus-architect
description: Architectural protocol for planning, documenting, and authoring precise tasks (The AST Nexus).
version: 1.0.0
---

# Nexus Architect (The AST Nexus)

## Overview
This skill outlines the protocol for architectural decision-making, specification writing, and creating precise, executable tasks for builders. It enforces that every feature is documented as a linked triad (ADR, SPEC, TASK) to maintain a robust architectural design.

---

## When to Use
Apply this skill when:
- Designing a new system feature or major architectural change.
- Creating or editing Architectural Decision Records (ADRs) under `docs/decisions/`.
- Authoring component specifications (SPECs) or task instructions (TASKs) for development.
- Conducting compliance audits on existing specs.

**When NOT to Use:**
- Writing actual production code or styling elements.
- Fixing trivial bugs or minor issues that do not modify system contracts.

---

## The AST Nexus Triad

Every feature must be documented as a linked triad (The AST Nexus) to ensure long-term maintainability and builder precision:

### 1. ADR (The "Why")
- Explains the motive, strategy, and technical trade-offs.
- References the SPEC in the `Implementation Guidance` section.
- Must document: Status, Context, Alternatives Considered (with reasons for rejection), Decision, Consequences, and Compliance.

### 2. SPEC (The "What")
- Defines the source of truth for UX, state behavior, and business logic.
- References the parent ADR in the header.

### 3. TASK (The "How")
- Provides atomic, executable instructions.
- Must contain a `Parent` header linking to BOTH the ADR and the SPEC.

---

## Task Authoring Protocol (The "Hand-off" Standard)
Tasks written for developers or subagents must be executable without further clarification and include:

1. **Definition of Done (DoD)**: Checkable list of outcomes.
2. **Technical Context**: Specific files, existing stores, or functions to modify.
3. **Draft Implementation Plan**: Step-by-step logic guide.
4. **Test Requirements**: Specific edge cases to cover with tests (TDD).
5. **Hazards**: Known blockers, side effects, or atomic transaction risks.

---

## Delegate Protocol: Behavioral Proposal
Before creating a TASK or starting implementation:
1. **Description**: Describe the feature behavior in Russian (User path + UI logic).
2. **Examples**: Provide 3-5 specific examples (e.g., Input: "..." -> Output: "...").
3. **Approval**: Present this to the User (Oleg). Proceed ONLY after receiving "OK" or "GO".
4. **Linkage**: Once approved, include the Proposal summary in the TASK.md.
