# CloudKey

A phase-based, multi-platform development toolkit for [Claude Code](https://code.claude.com).
One plugin, organized by SDLC phase, with dedicated skills for the platforms you actually ship on.

## Install

```bash
/plugin marketplace add webdevdot/cloudkey
/plugin install cloudkey@cloudkey
```

## What's inside

### Phase skills (the SDLC, in order)
| Skill | Phase |
|-------|-------|
| `/plan` | Understand & scope; route to the right platform |
| `/scaffold` | Stand up a runnable skeleton |
| `/implement` | Build in small increments (uses the `architect` agent) |
| `/test` | lint + test + build to green |
| `/review` | Read-only correctness + simplicity + security pass |
| `/deploy` | Ship, gated on green test + review |

### Platform skills
| Skill | Covers |
|-------|--------|
| `/shopify-dev` | Themes/Liquid, Hydrogen, Admin & Storefront GraphQL, Functions, extensions |
| `/nextjs-dev` | App Router, server components, Route Handlers, Vercel |
| `/ai-app-dev` | Claude API, agents, tool use, RAG, prompt design |
| `/code-index` | Symbol & semantic search before changing code (uses the `indexer` agent) |
| `/document` | Generate/update docs (README, API ref, doc comments) accurate to the code |
| `/refactor` | Behavior-preserving cleanup; tests stay green throughout |
| `/design` | UI/UX: Figma↔code via Figma MCP + web interface best practices (uses `design-reviewer`) |
| `/audit` | Run a wide, repo-scale task as a **dynamic workflow** (high fan-out, runs in background) |
| `/orchestrate` | The **conductor** — runs a feature end to end, delegating each phase to the right agent |

### The Code Agent Orchestra
`/orchestrate` is the conductor: it holds the plan and decides which agent plays next, threading a
feature through plan → design → implement → test → review → deploy with **explicit handoffs**. What
makes the multi-agent loop actually work, and is enforced by the skill:
- **One writer** — only the `coder` agent edits code; testers/reviewers are read-only.
- **Narrow context** — each agent gets only the artifact it needs (diff, failing output, frame).
- **Typed handoffs** — every phase ends with a concrete artifact the next phase consumes.
- **Stop conditions** — done = lint+test+build green AND review PASS; no looping the same failure twice.
- **Persistent agent memory** — `architect`, `indexer`, and `design-reviewer` carry `memory: project`,
  so they recall this repo's patterns and recurring issues across runs (`.claude/agent-memory/`).

### Workflows vs skills
CloudKey's phase skills are for **interactive, reviewed** development — Claude follows them turn by
turn. For **wide, deterministic** tasks (audit every file, migrate across the repo, cross-checked
research), use `/audit`, which triggers a [dynamic workflow](https://code.claude.com/docs/en/workflows):
a JS orchestration script the runtime runs in the background across dozens–hundreds of agents, keeping
intermediate results out of context. Run it, then save the run with `/workflows` → `s` for reuse.

### Agents
- **architect** — read-only design pass for a feature.
- **indexer** — fast read-only fan-out codebase search.
- **design-reviewer** — read-only UI/UX critique (a11y, responsiveness, states, composition).
- **debugger** — systematic root-cause debugging (reproduce → isolate → confirm → propose fix).
- **security-reviewer** — read-only security review (injection, authz, secrets, deps).

### Bundled MCP
- **context7** (`@upstash/context7-mcp`) — live, version-correct library docs. Free, no API key for
  the public tier. The `nextjs-dev`, `ai-app-dev`, and `design` skills route to it for current API syntax.
- **github** (`@modelcontextprotocol/server-github`) — PRs, issues, code search. Reads its token from
  the `GITHUB_TOKEN` env var (never stored in the plugin). Without a token it works for public reads.
- **shopify-dev** (`@shopify/dev-mcp`) — official Shopify Dev MCP: live Admin/Storefront GraphQL schema
  introspection + docs search. Read-only, no auth. Powers the `/shopify-dev` skill's schema verification.

> **Not bundled on purpose:** a database MCP (Postgres/SQLite). It needs a per-project connection
> string that doesn't belong in a shared plugin. Add it per-project when you need it:
> `claude mcp add --scope local postgres -- npx -y @modelcontextprotocol/server-postgres "$DATABASE_URL"`.
> This keeps CloudKey's tool surface lean — bundling DB tools into every install would hurt tool selection.

## Design notes
- **Phase-based, not a tool dump.** ~12 focused skills instead of hundreds, to avoid tool bloat that
  degrades model tool selection.
- **Reuse over duplication.** Platform skills route to authoritative installed skills (the Shopify
  plugin, `claude-api`, Context7/`find-docs`) and to the `loop-engineering` plugin's tester/reviewer
  agents when present — rather than re-implementing them.

MIT © webdevdot
