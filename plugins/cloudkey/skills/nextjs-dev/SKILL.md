---
name: nextjs-dev
description: Next.js / React development — App Router, server components, routing, data fetching, and Vercel deployment.
---

# Next.js / React development

Use for any Next.js or React work in a CloudKey phase.

Conventions:
- **App Router by default** (`app/` dir). Server Components are the default; mark Client Components
  with `"use client"` only where interactivity/state/browser APIs are needed.
- **Data fetching** in Server Components; use Route Handlers (`app/api/.../route.ts`) for endpoints.
- **Scaffold** with `npx create-next-app@latest` (TypeScript, App Router, ESLint).
- **Validation**: `next lint`, the project's test runner, `next build`.
- **Deploy**: `vercel deploy` (preview) / `vercel --prod`, or push to trigger the CI workflow.

ALWAYS confirm current Next.js / React API syntax against live docs via `find-docs` (Context7) before
writing — App Router APIs change between versions and training data may be stale. Do not guess config
or API signatures.
