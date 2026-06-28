---
name: document
description: Generate or update documentation for code — READMEs, API references, doc comments, and changelogs — kept accurate to the actual implementation.
---

# Document

Goal: produce or refresh docs for **$ARGUMENTS** that match what the code actually does.

1. **Read the code first.** Document the real behavior, signatures, and edge cases — never describe
   intended behavior the code doesn't have. If code and existing docs disagree, surface it.
2. **Pick the artifact**: README section, API reference, inline doc comments (JSDoc/docstrings), or a
   CHANGELOG entry. Match the project's existing doc style and format.
3. **Be concrete**: real examples that run, accurate parameter/return types, and the error/edge cases a
   caller must handle. Prefer short and correct over long and vague.
4. **Verify** any framework/API references against current docs via `find-docs` (context7) rather than memory.
5. Keep docs next to what they describe and update them in the same change as the code.

Output: the doc content (or the edits to make), plus a note of anything where code and prior docs conflicted.
