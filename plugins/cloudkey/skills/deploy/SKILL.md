---
name: deploy
description: Phase 6 of the CloudKey SDLC. Ship the change, gated on a green test + review, with a platform-appropriate deploy path.
---

# Phase 6 — Deploy

Goal: ship **$ARGUMENTS** safely. Deploy ONLY when `/test` is green and `/review` returned PASS.

1. **Gate**: re-confirm lint + test + build pass and review approved. If not, stop and route back.
2. **Pick the deploy path** for the platform:
   - Shopify app/extension → `shopify app deploy`; theme → `shopify theme push`.
   - Next.js → `vercel deploy` (or the project's configured target).
   - AI/LLM service → the project's container/host deploy.
   - Library → `npm publish`.
3. **Prefer CI**: if a GitHub Actions workflow exists, push to trigger the gated deploy rather than
   deploying from your machine. Surface the run URL.
4. **Confirm** the deploy succeeded (health check / URL) and report what shipped.

Deploys are outward-facing — confirm with the user before triggering a production deploy unless they
have already authorized it.
