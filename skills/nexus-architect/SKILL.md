---
name: nexus-architect
description: Plan GTDing changes, author ADR/SPEC contracts, and create precise self-contained GitHub Issues for implementation. Use when designing behavior or architecture, writing or reviewing docs/decisions and docs/specs, decomposing approved work into executable issues, or auditing task quality and dependencies.
---

# Nexus Architect

Treat GitHub Issues as the only source of truth for task identity, lifecycle, priority, execution profile, and dependencies. Keep architectural context versioned in the repository.

Before authoring work, read the repository's current `AGENTS.md`. In GTDing also read:

- `docs/decisions/030-github-issues-task-tracking.md`
- `docs/specs/030-github-issues-task-tracking.md`
- `.github/ISSUE_TEMPLATE/task.yml`

Repository instructions override this skill when they are more specific.

## Architecture chain

Use the smallest complete chain appropriate to the change:

1. **ADR — why:** record a durable decision, alternatives, consequences, and compliance for new architecture, public interfaces, or meaningful trade-offs.
2. **SPEC — what:** define observable behavior, boundaries, state transitions, failure behavior, and acceptance criteria. Link its parent ADR.
3. **GitHub Issue — executable hand-off:** define how to deliver one bounded outcome. Link the merged ADR/SPEC by exact repository-relative paths.
4. **Pull Request — review and closure:** implement the Issue and include `Closes #NNN`. Merge, not task-file movement, closes the Issue.

Do not create an ADR/SPEC merely to satisfy ceremony for a contract-free bug or chore. In that case use a reasoned `N/A — <reason>` in the Issue parent fields.

## Planning workflow

For new behavior, interfaces, or architecture:

1. Surface material assumptions and convert the request into measurable success criteria.
2. If intent remains ambiguous, pause and use `interview-me` before designing.
3. Create or update ADR/SPEC on a planning branch. Do not modify application code in this phase.
4. Push the documents and open a planning PR against the exact branch of origin.
5. End the planning hand-off with the repository-required approval marker. In GTDing use exactly `[СТАТУС: ОЖИДАНИЕ АППРУВА]`.
6. After the architecture PR is merged, create the executable Issue through `.github/ISSUE_TEMPLATE/task.yml` and leave it in `status:triage` until explicitly approved.

Never create `tasks/TASK-*.md`, choose a `TASK-NNN` identifier, restore `tasks/INDEX.md`, or treat `docs/archive/tasks/` as executable work. GitHub assigns the Issue number.

## Issue contract

Write for an executor with no chat history. A task Issue must contain:

- `Parent ADR`: existing `docs/decisions/*.md`, or reasoned `N/A` for a contract-free bug/chore;
- `Parent SPEC`: existing `docs/specs/*.md`, or reasoned `N/A`;
- `User outcome`: observable result for a user, operator, or maintainer;
- `Technical context`: exact boundaries, files, routes, stores, functions, external systems, and preserved contracts;
- `Definition of Done`: independently checkable outcomes, including negative and compatibility expectations;
- `Test requirements`: concrete positive, negative, regression, integration, and browser checks proportional to risk;
- `Hazards`: data-loss, security, concurrency, migration, compatibility, UX risks, and forbidden shortcuts;
- `Priority`: `P0`, `P1`, `P2`, or `P3`;
- `Primary model`: default `GPT-5.6 Sol`;
- `Reasoning effort`: `low`, `medium`, `high`, `xhigh`, `max`, or `ultra`;
- `Gemini delegation`: `safe with validation`, `conditional`, or `do not delegate`;
- `Required validation`: independent reviewer and exact evidence to inspect;
- `Dependencies`: Issue references and external prerequisites, or `None`.

Do not duplicate the complete ADR/SPEC inside the Issue. Include enough technical context that the executor knows what to inspect and what not to change.

## Execution profile

Default to GPT-5.6 Sol. Choose reasoning from workload risk, not task size alone:

- `low`: verification, tiny localized edits, deterministic cleanup;
- `medium`: bounded implementation with familiar patterns;
- `high`: multi-file behavior, reviews, CI/tooling, non-trivial UX;
- `xhigh`: cross-module work, migrations, release-critical integration;
- `max` or `ultra`: destructive data paths, security boundaries, production rollout, or decisions with expensive failure.

Use Gemini only when the Issue has explicit boundaries and validation:

- `safe with validation`: the whole bounded task may be delegated; Sol independently reviews the diff and evidence;
- `conditional`: delegate only named slices, preserving Sol ownership of integration or risky decisions;
- `do not delegate`: keep destructive, security-sensitive, architectural, or production actions with Sol/human review.

## Dependencies and hierarchy

- Use native GitHub `blocked by` relationships for causal blockers.
- Use native sub-issues for an epic or initiative.
- Keep external approvals in `Dependencies` and use `status:blocked` when they prevent execution.
- Do not infer a blocker merely because another Issue is mentioned.
- Treat GitHub Project fields as a portfolio view; Issue body, labels, and native relationships remain authoritative.

## Lifecycle

Maintain exactly one lifecycle label:

1. `status:triage` — authored but not approved;
2. `status:ready` — approved and unblocked;
3. `status:in-progress` — implementation started;
4. `status:blocked` — dependency or decision prevents progress;
5. `status:in-review` — PR opened with `Closes #NNN`;
6. closed/Done — PR merged.

Creating an Issue is not implementation approval. Start code only after `status:ready` or explicit user approval.

## Quality audit

Reject or refine an Issue when any of these are true:

- the outcome is phrased only as code changes;
- ADR/SPEC paths are placeholders, missing, or escape the repository;
- DoD cannot be checked independently;
- tests say only "add tests" without scenarios;
- hazards omit an obvious destructive or compatibility risk;
- implementation requires hidden chat context;
- priority, reasoning, or delegation lacks a defensible risk basis;
- multiple lifecycle labels exist;
- dependencies are prose-only despite having corresponding Issues;
- the Issue recreates a legacy `TASK-NNN` identity or file.

Finish by stating what was authored, which assumptions remain, the approval state, and the next permitted action.
