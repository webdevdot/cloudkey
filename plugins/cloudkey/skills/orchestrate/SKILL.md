---
name: orchestrate
description: The conductor of CloudKey's multi-agent orchestra. Runs a feature end to end through plan → design → implement → test → review, delegating each phase to the right specialized agent with explicit handoffs.
---

# Orchestrate (the conductor)

Goal: take **$ARGUMENTS** from idea to shipped, coordinating CloudKey's agents so each one does the
narrow thing it's best at and the result of each phase is handed cleanly to the next.

This skill is the *conductor* — it holds the plan and decides who plays next. The agents are the
*players*. What makes the orchestra work is the discipline below, not just having many agents.

## The score (phase → who plays → handoff)

1. **Understand** — if the codebase is unfamiliar, delegate to `indexer` to map the relevant files and
   symbols. Handoff: a short location map.
2. **Plan** — run `/plan` (or delegate design to `architect`). Handoff: approach + ordered steps + files.
3. **Design** (UI work only) — run `/design`; for a critique delegate to `design-reviewer`.
   Handoff: implemented/specified UI + which best-practice checks pass.
4. **Implement** — run `/implement`; the only writer is the `coder` agent (from `loop-engineering` if
   installed). Make the *smallest* useful change per step. Handoff: the diff.
5. **Test** — run `/test`; delegate to `tester`. Handoff: `ALL GREEN` or `RED: <checks>` with output.
6. **Review** — delegate to `reviewer` (correctness/simplicity) and, for UI, `design-reviewer`.
   Handoff: `PASS` or `CHANGES-REQUESTED` + list.
7. **Loop or ship** — on RED or CHANGES-REQUESTED, return to step 4 with the specific feedback. When
   test is green AND review is PASS, run `/deploy` (gated).

## What makes multi-agent coding actually work (enforce these)
- **One writer.** Only `coder` edits code. Reviewers and testers are read-only. This prevents two
  agents fighting over the same file and keeps blame clear.
- **Narrow context per agent.** Hand each agent only what it needs (the diff, the failing output, the
  target frame) — not the whole history. Fresh context windows are the point of subagents.
- **Explicit handoffs.** Every phase ends with a typed artifact (location map, plan, diff, test verdict,
  review verdict). The next phase consumes that artifact, not a vague "continue."
- **Stop conditions.** Define done up front: lint + test + build green AND review PASS. Don't loop on the
  same failure more than twice without escalating to the user.
- **Persistent memory.** The agents carry `memory: project`, so they recall this repo's patterns and
  recurring issues across runs. Trust and update that memory rather than re-deriving every time.

## When to hand off to a workflow instead
If the task is wide and deterministic (audit/migrate/research across many files), don't conduct it turn
by turn — run `/audit` to spin up a dynamic workflow. Use this conductor for interactive feature work.
