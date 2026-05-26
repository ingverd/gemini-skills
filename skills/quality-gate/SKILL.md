---
name: quality-gate
description: Protocol for verifying task completion. Ensures the implementation is fully functional, aligns with the specification, and leaves no technical debt.
version: 1.0.0
---

# Quality Gate (The Verification Protocol)

## Overview
This skill defines the verification process to ensure that newly written code is not just logically correct, but fully functional, robust, and aligned 1:1 with the original technical specification before it is merged.

---

## When to Use
Apply this skill when:
- A builder subagent or peer agent claims a task is completed.
- Preparing to merge a feature branch back into the main branch.
- Verifying the final state of an implementation plan.

---

## The 5-Step Verification Process

### 1. Functional Verification (The "Does it Run?" Test)
- **Runtime Check**: Verify that the application builds and runs in the local environment without errors.
- **Side-Effect Audit**: Audit changes to ensure they did not introduce regression bugs in unrelated modules.

### 2. Specification Alignment
- Compare the actual code and UI behavior against the corresponding **SPEC** file.
- Check that all designated edge cases mentioned in the ADR or SPEC are fully handled.
- Ensure any specific UI flow matches the exact description in the spec.

### 3. The "Broken Link" Check
- Verify that new files, components, and pages are correctly wired up and accessible via the specified routes.
- Ensure no "TODO" or placeholder comments are left in production code.

### 4. Visual Verification (The Browser Test)
- For all UI-related changes, run the project dev server and perform an audit using automated browser tools or manual verification.
- Capture visual evidence (e.g. screenshots) of the new feature working as intended.
- Stop all running dev servers and background processes when verification is complete.

### 5. Final Hand-off
- Only when all previous checks are green, submit the final verification results (e.g. a walkthrough) and present them for review.

---

## Acceptance Criteria Checklist
Before code is considered fully done:
- [ ] Tests pass in both local and CI environments.
- [ ] Runtime execution demonstrates that the feature is fully operational.
- [ ] Code logic matches the specification 1:1.
- [ ] Documentation is completely updated to reflect the final state.
