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
| `/design` | UI/UX: Figma↔code via Figma MCP + web interface best practices (uses `design-reviewer`) |
| `/audit` | Run a wide, repo-scale task as a **dynamic workflow** (high fan-out, runs in background) |

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

### Bundled MCP
- **context7** (`@upstash/context7-mcp`) — live, version-correct library docs. Free, no API key for
  the public tier. Ships with the plugin so it's self-contained: the `nextjs-dev`, `ai-app-dev`, and
  `design` skills route to it for current API syntax instead of relying on stale training data.

## Design notes
- **Phase-based, not a tool dump.** ~12 focused skills instead of hundreds, to avoid tool bloat that
  degrades model tool selection.
- **Reuse over duplication.** Platform skills route to authoritative installed skills (the Shopify
  plugin, `claude-api`, Context7/`find-docs`) and to the `loop-engineering` plugin's tester/reviewer
  agents when present — rather than re-implementing them.

MIT © webdevdot
