---
name: code-simplification
description: Refactor code for maximum readability, maintainability, and clarity. Enforces strict behavior preservation and the Chesterton's Fence principle.
version: 1.0.0
---

# Code Simplification & Refactoring

## Overview
The primary goal of this skill is **Clarity over Cleverness (Понятность важнее краткости)**. Code must be easy to read, modify, and debug. Every simplification we apply must answer yes to the test: *"Будет ли новый разработчик команды понимать этот код быстрее, чем исходную версию?"*

---

## When to Use
Apply this skill when:
- Conducting post-feature cleanups before committing and submitting a Pull Request.
- Refactoring functional but overly complex methods, long functions, or tangled Zustand actions.
- Reviewing existing codebase files to reduce technical debt.
- Simplifying complex boolean logic, loops, or conditional branching.

**When NOT to Use:**
- When the original behavior of a piece of code is not fully understood.
- When there are no automated tests (Vitest) covering the affected code (write tests first!).
- Changing the inputs, outputs, side effects, or error states of existing methods.

---

## Core Refactoring Principles

### 1. Preserve Behavior Exactly
- All inputs, outputs, error pathways, side effects, and exact edge case results must remain completely identical.
- If any behavior change is needed, it belongs in a feature/fix branch, not in a simplification cleanup.

### 2. Chesterton's Fence (Забор Честертона)
- **Rule**: Never remove or completely rewrite a line of code or logic block until you fully understand *why* it was placed there in the first place.
- **Action**: Research git blame, commit history, or comments to find the context behind complex logic before touching it.

### 3. Incremental Changes (Микро-шаги)
- Simplify one tiny chunk at a time. 
- Run `npx vitest run` immediately after every micro-change. Never rewrite 100 lines at once and then try to figure out why everything broke.

### 4. Readability > Dense Code
- Prefer clean, explicit, self-documenting code over clever, compressed inline "magic" tricks (e.g., heavily nested ternary operators or complex single-line regular expressions).

---

## Step-by-Step Refactoring Process

### Step 1: Safety Setup
- Verify that the code being simplified has a solid test suite.
- If coverage is poor, write 3-5 unit tests covering edge cases before making any changes.

### Step 2: Formulate the Refactoring Hypothesis
- State clearly what part of the file is complex and how you plan to simplify it (e.g., *"Extract task filtering logic into a separate helper function to decrease TaskList component complexity"*).

### Step 3: Execute Incremental Simplification
- Apply the changes in small, isolated steps.
- Run tests (`npx vitest run`) and check typings after each step.

### Step 4: Verification Gate
- Run full typecheck and linting:
  ```bash
  npx tsc --noEmit
  npm run lint
  ```
- Ensure zero errors or warnings before committing.
