---
name: implement
description: Phase 3 of the CloudKey SDLC. Build the feature in the smallest useful increments, delegating to the architect agent for design.
---

# Phase 3 — Implement

Goal: build **$ARGUMENTS** in small, verifiable increments.

1. Take the plan from `/plan`. For any non-trivial design decision, consult the `architect` agent
   (`subagent_type: "architect"`) for a focused design before coding.
2. Make the **smallest useful change** that advances the feature. Match surrounding code style; reuse
   existing utilities; prefer the platform skill's idioms (`/shopify-dev`, `/nextjs-dev`, `/ai-app-dev`).
3. After each increment, run `/test`. Do not pile up untested changes.
4. Repeat until the feature is complete, then hand off to `/review`.

Do not declare done here — `/test` and `/review` own that judgment.
