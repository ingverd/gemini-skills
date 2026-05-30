---
name: dev-workflow
description: Develop high-quality code using strict TDD, feature-branch isolation, and structured quality gates in the GTDing project.
version: 1.2.0
---

# GTD Development Workflow (Builder Edition)

## Overview
This skill implements the strict 9-stage implementation loop for the `gtding` project. It incorporates architectural guardrails (Stage 0: Behavioral Proposal) and Test-Driven Development (TDD) with strict quality gates (TypeScript checking, ESLint, and Vitest) to ensure production-grade software delivery.

---

## When to Use
Apply this skill when:
- Implementing any new features or components in the `gtding` project based on existing tasks or plans.
- Fixing bugs, refactoring logic, or modifying app behavior.
- Working on specific implementation items listed in `task.md`.

**When NOT to Use:**
- Writing standalone documentation or ADRs.
- Simple administrative tasks (e.g., updating dependencies in `package.json` without code impact).
- Minor design mockups that do not involve active logic changes.

---

## Core Rules

1. **Instruction First**: Work ONLY from the tasks specified in `task.md` or assigned task files. You are an executor.
2. **Minimalism**: Write only what is requested. Move from Red to Green as fast as possible.
3. **No Architecture**: Do not modify ADRs or Specs unless explicitly told to do so in the TASK.
4. **No Modals**: Everything uses routes! No modal windows are allowed in this project.
5. **Clean Commits**: Commit messages must adhere to the `conventional-commits` skill.
6. **No Direct Commits**: Never push or commit directly to the `master` branch. Always work on isolated feature branches.

---

## The 9-Step Implementation Loop

### Stage 0: Behavioral Proposal (Architectural Guardrail)
*   **Action**: Before writing any code, document the intended behavior in Russian.
*   **Requirements**: Describe the "User Path", UI reactions, and 3-5 Edge Cases with Input/Output examples.
*   **Exit Criteria**: Submit the proposal to the user (Oleg) and wait for explicit approval ("OK" or "GO").

### Stage 1: Analyze Task
*   Read the assigned task details or `task.md`.
*   Ensure you fully understand the criteria, expectations, and the Definition of Done (DoD).

### Stage 2: Branching
*   Create an isolated feature branch using the format:
  ```bash
  git checkout -b feature/NNN-task-description
  ```
  *(Replace NNN with the task or issue number)*

### Stage 3: TDD - Red
*   Write a failing test for the requested logic or component behavior before writing any production code.
*   Run `npx vitest run` to verify the test fails for the expected reasons.

### Stage 4: Implementation
*   Write the minimal production code necessary to make the failing test pass.
*   Do not add speculative features or build unrequested abstractions.

### Stage 5: TDD - Green
*   Run `npx vitest run` and ensure all tests are now passing successfully.

### Stage 6: Refactor
*   Clean up, simplify, and polish the newly added code.
*   Ensure proper variable names, layout, and comments are maintained.
*   Run tests again to ensure the refactoring did not break anything.

### Stage 7: Verification
*   Run typecheck and lint tools to ensure perfect code health:
  ```bash
  npx tsc --noEmit
  npm run lint
  ```
*   Address and fix any warnings or errors immediately.

### Stage 8: Commit & PR
*   Format your commit message according to the `conventional-commits` skill.
*   **PR Title Format**: The PR title MUST include the task number if one exists (e.g., `feat(store): TASK-011: implement dynamic entity store`).
*   **PR Description Format**: The PR description MUST be structured strictly in Russian using the following template:
    ```markdown
    ## Что сделано

    - [Описание изменения 1]
    - [Описание изменения 2]

    ## 🔍 Как проверить

    1. [Шаг 1 проверки (ручной сценарий в браузере/UI, никаких автоматических тестов/линтеров!)]
    2. [Шаг 2 проверки]
    ```
    **PR Description Rule (CRITICAL)**: The "🔍 Как проверить" (How to verify) section in the Pull Request body MUST contain ONLY manual verification steps in the UI/browser. Do NOT list automated checks (such as `vitest`, `tsc`, or `eslint`).
*   **PowerShell PR Creation Hygiene (CRITICAL)**: PowerShell's double quotes parse backtick (`` ` ``) and backslash (`\`) as escape characters. To prevent broken markdown encoding, swallowed characters, or split lists:
    1. **NEVER** write long multi-line bodies directly as command arguments (`gh pr create --body "..."`).
    2. **ALWAYS** write the PR body to a temporary file (e.g. `tasks/temp_pr_body.md`).
    3. **ALWAYS** run: `$env:GITHUB_TOKEN=$null; gh pr create --body-file tasks/temp_pr_body.md` or `gh pr edit <PR> --body-file tasks/temp_pr_body.md`.
    4. **ALWAYS** delete the temporary file after creation/edit completes.

---

## Definition of Done (DoD)
Before completing the task and submitting the branch, ensure:
- [ ] The behavioral proposal was approved by Oleg.
- [ ] The code strictly matches the implementation plan.
- [ ] TDD cycle is fully completed (failing and passing tests are committed).
- [ ] Zero TypeScript errors (`npx tsc --noEmit` passes).
- [ ] Zero linting errors (`npm run lint` passes).
- [ ] All tests pass successfully (`npx vitest run`).
- [ ] Documentation is updated if applicable (`node scripts/generate-docs.js`).
- [ ] Commit messages follow the Conventional Commit standard.
