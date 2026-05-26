---
name: conventional-commits
description: Standard for commit messages based on Conventional Commits, with project-specific scopes and rules.
version: 1.0.0
persistence:
  rules:
    - Всегда используй этот формат для коммитов в репозитории gtding.
    - Типы: feat, fix, refactor, style, test, docs, chore, perf, ci.
    - Scope должен быть осмысленным (tasks, projects, ui, store и т.д.).
---

# Conventional Commits

## Overview
This skill defines the strict formatting standard for commit messages in the `gtding` project. Clean, well-structured, and typed commit logs enable automated release generation, easy rollback tracing, and instant understanding of the codebase history.

---

## Commit Format

Each commit message must consist of a **header**, a **body**, and a **footer**. The header has a special format that includes a **type**, a **scope**, and a **subject**:

```
<type>(<scope>): <subject>

[optional body]

[optional footer(s)]
```

### Types (Типы коммитов)
You must categorize changes using one of the following types:
- `feat`: A new feature or user-facing capability.
- `fix`: A bug fix or correction.
- `refactor`: Code change that neither fixes a bug nor adds a feature (cleanups, restructuring).
- `style`: Changes that do not affect the meaning of the code (formatting, missing semi-colons, white-space).
- `test`: Adding missing tests or correcting existing tests.
- `docs`: Documentation only changes.
- `chore`: Updating build tasks, package manager configs, or internal utilities (no production code changes).
- `perf`: A code change that improves performance.
- `ci`: Changes to our CI configuration files and scripts.

### Meaningful Scopes (Осмысленный Scope)
The scope must specify the exact area of the codebase being affected. Examples:
- `ui`: Changes related to buttons, components, views, or Ant Design styling.
- `store`: Zustand state management, actions, or Immer logic.
- `router`: React Router routes, navigation, or transition guards.
- `tasks`: Task management components, parsers, or states.
- `projects`: Project management logic or pages.
- `tests`: Test configuration or E2E scripts.
- `docs`: Development guidelines or manual files.

---

## Examples

### Good Commits
- `feat(ui): add new routed page for task editing`
- `fix(store): resolve infinite loop when updating active tasks`
- `refactor(tasks): simplify markdown parsing logic for code blocks`
- `test(store): add unit tests for zustand state changes under immer`

### Bad Commits (Avoid!)
- `fix: fixed stuff` (missing scope and vague subject)
- `added new screen` (missing type, scope, and wrong casing)
- `feat(custom-modals): add task editing popup` (violates both meaningful scope and the **No Modals** rule!)
