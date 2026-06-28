---
name: scaffold
description: Phase 2 of the CloudKey SDLC. Create the initial project skeleton for the chosen platform.
---

# Phase 2 — Scaffold

Goal: stand up a runnable skeleton for **$ARGUMENTS** on the detected platform.

1. Confirm the platform from `/plan`. Use the matching platform skill for idiomatic scaffolding:
   - Shopify → `/shopify-dev` (Shopify CLI app/theme/extension scaffolds)
   - Next.js → `/nextjs-dev` (`create-next-app`, App Router layout)
   - AI/LLM → `/ai-app-dev` (Claude SDK project skeleton)
2. Initialize version control and a `.gitignore` if not present.
3. Add the project's three validation commands to `package.json` (or equivalent): **lint, test, build**.
4. Create one trivial passing test so the test runner is wired up.
5. Verify the skeleton runs (dev server boots / build succeeds), then hand off to `/implement`.

Keep the scaffold minimal — no speculative features. The point is a green, runnable baseline.
