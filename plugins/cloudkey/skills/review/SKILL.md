---
name: review
description: Phase 5 of the CloudKey SDLC. Read-only review for correctness, simplicity, and platform best practices.
---

# Phase 5 — Review

Goal: a read-only quality pass on **$ARGUMENTS** once `/test` is green.

Check:
- **Correctness** — does it implement what was asked? Edge cases (empty, zero, negative, error paths)?
- **Simplicity** — smallest reasonable change? Any duplication, dead code, or needless abstraction?
- **Platform best practices** — consult the relevant skill: `/shopify-dev`, `/nextjs-dev`, `/ai-app-dev`.
- **Security** — secrets not committed, inputs validated, deps current.

Return a verdict on the final line: `PASS` or `CHANGES-REQUESTED` + a short specific list.
On CHANGES-REQUESTED, hand back to `/implement`. On PASS, hand off to `/deploy`.

Do not edit code here. If `loop-engineering` is installed, delegate to its `reviewer` agent.
