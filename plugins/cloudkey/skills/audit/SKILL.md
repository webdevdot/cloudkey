---
name: audit
description: Run a high-fan-out, repo-wide task as a dynamic workflow — codebase audits, large migrations, or cross-checked research that needs more agents than one conversation can coordinate.
---

# Audit (dynamic workflow)

Use when a CloudKey task is **wide and deterministic** rather than interactive: auditing every file
for a problem, a large migration, or research cross-checked across many sources. This is the case
where a **workflow** beats turn-by-turn skills/agents — the orchestration runs as a script, results
stay in script variables, and it scales to dozens–hundreds of agents without flooding context.

## When to use this vs the phase skills
- **Phase skills** (`/plan` … `/deploy`): interactive feature work you review step by step.
- **`/audit` (workflow)**: one wide pass over many files/sources, run in the background, one report out.

## How to run
Trigger a dynamic workflow for **$ARGUMENTS** by including the `ultracode` keyword (or asking for a
"workflow") so Claude writes and runs an orchestration script instead of working turn by turn:

```
ultracode: <the wide task, e.g. "audit every route under src/ for missing auth checks">
```

Watch progress with `/workflows`. When the run does what you want, **save it** for reuse: in the
`/workflows` view select the run and press `s` → save to `.claude/workflows/` (repo-shared) or
`~/.claude/workflows/` (personal). It then runs as its own `/command`.

## Notes
- Requires Claude Code v2.1.154+ and a paid plan; enable Dynamic workflows in `/config` on Pro.
- Workflows spawn many agents and cost more tokens — try a small slice first (one dir, narrow question).
- The script can't touch the shell/filesystem directly; its agents do the work. For per-stage sign-off,
  run each stage as its own workflow.
- For a quality pattern, ask for agents that adversarially review each other's findings before reporting.
