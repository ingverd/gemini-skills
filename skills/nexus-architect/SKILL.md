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

### 4. Pull Request (The "Review")
- After authoring, committing, and pushing the AST Triad documents, you MUST create a Pull Request (using `gh pr create` or similar) so the User can formally review and approve the architectural decisions before any implementation begins.

---

## Task Authoring Protocol (The "Hand-off" Standard)
Tasks written for developers or subagents must be executable without further clarification and include:

1. **Definition of Done (DoD)**: Checkable list of outcomes.
2. **Technical Context**: Specific files, existing stores, or functions to modify.
3. **Draft Implementation Plan**: Step-by-step logic guide.
4. **Test Requirements**: Specific edge cases to cover with tests (TDD).
5. **Hazards**: Known blockers, side effects, or atomic transaction risks.

---

## Pipeline Synergy: Interview-Me -> Nexus-Architect

**CRITICAL**: There is an intentional, synergistic loop between `/interview-me` and `/nexus-architect`. This is NOT a conflicting circular dependency. They form a two-step pipeline for building the right thing:

1. **Extraction (`/interview-me`)**: Used *first* when the ask is vague, ambiguous, or underspecified. Its goal is to extract the *true intent* and finalize the requirements.
2. **Architecture (`/nexus-architect`)**: Used *second* once requirements are clear (either explicitly provided or extracted via the interview). Its goal is to translate that intent into concrete system design (ADR, SPEC, TASK).

**The Loop**: If you start with `/nexus-architect` and immediately realize the requirements are too vague or you are making too many assumptions, you MUST pause and invoke `/interview-me` to clarify intent. Conversely, `/interview-me` explicitly instructs you to transition to `/nexus-architect` once the interview is complete. Always prefer to use BOTH skills sequentially for major features.
