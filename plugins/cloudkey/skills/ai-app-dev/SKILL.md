---
name: ai-app-dev
description: Building AI/LLM applications — Claude API integration, agents, tool use, RAG, and prompt design.
---

# AI / LLM app development

Use for building AI features in a CloudKey phase.

Defaults (this is an Anthropic-first toolkit):
- **Model**: default to the latest capable Claude model for the task. Use the `claude-api` skill /
  `find-docs` for current model IDs, pricing, and parameters — never hardcode from memory.
- **SDK**: `@anthropic-ai/sdk` (TS) or `anthropic` (Python). Keep the API key in env, never in code.
- **Agents / tool use**: define tools with clear JSON schemas; keep the tool set small and focused.
- **RAG**: chunk → embed → retrieve → ground the prompt in retrieved context with citations.
- **Streaming**: stream responses for UX; handle tool-call and stop-reason events explicitly.
- **Evaluation**: add an LLM-judge or assertion-based eval before shipping prompt changes.

For provider/model/pricing/caching/tool-use questions, consult the `claude-api` skill or `find-docs`
rather than answering from memory — these change frequently.
