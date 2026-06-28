---
name: code-index
description: Build and query a fast index of a codebase for symbol lookup and semantic search before making changes.
---

# Code indexing & search

Use to understand an unfamiliar or large codebase before planning/implementing.

Approach (prefer fast, local tools — no paid services):
1. **Structure first**: map the tree and entry points with `Glob` / the filesystem MCP
   (`mcp__filesystem__directory_tree`), and `Grep` for definitions.
2. **Symbol search**: ripgrep patterns for function/class/export definitions and their call sites.
   Build a short map of "where X lives / who calls X" rather than reading whole files.
3. **Semantic search** (optional): if a tree-sitter / embedding indexer is available in the repo
   (e.g. the toolkit's AST code-memory), use it; otherwise structural search above is sufficient.
4. **Delegate** broad fan-out searches to the `indexer` agent (`subagent_type: "indexer"`) so the main
   context stays clean — it returns the conclusion (paths + symbols), not file dumps.

Output a concise index: key modules, public API surface, and the files relevant to the current task.
Hand the findings to `/plan`.
