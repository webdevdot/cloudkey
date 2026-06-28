---
name: refactor
description: Behavior-preserving code cleanup — improve structure, naming, and duplication without changing what the code does. Tests must stay green throughout.
---

# Refactor

Goal: improve the internals of **$ARGUMENTS** without changing observable behavior.

The one rule: **behavior must not change.** Refactoring is not a rewrite and not a feature change.

1. **Green first.** Confirm tests pass *before* you start (`/test`). If there are no tests for the code
   you're about to change, add characterization tests first — you can't refactor safely without them.
2. **Small steps.** One transformation at a time: rename, extract function, remove duplication, simplify
   a conditional, narrow a type. Run tests after each step. Never batch many changes between test runs.
3. **No scope creep.** Don't fix bugs or add features mid-refactor — note them separately for `/implement`.
4. **Keep it green.** If a step turns tests red, the refactor changed behavior — revert that step and redo it.
5. Hand the result to `/review` (and `security-reviewer` if the touched code handles input/auth).

Prefer the smallest set of changes that removes the actual pain. Don't refactor code that isn't in your way.
