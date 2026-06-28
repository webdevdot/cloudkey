---
name: plan
description: Phase 1 of the CloudKey SDLC. Turn a request into a concrete, reviewed implementation plan before any code is written.
---

# Phase 1 — Plan

Goal: produce a clear, scoped plan for **$ARGUMENTS** before writing code.

1. **Understand** the request. Read the relevant code and docs. Identify existing functions,
   utilities, and patterns to reuse — never plan new code where suitable code already exists.
2. **Detect the platform** so later phases pick the right skill:
   - Shopify (theme/Liquid, Hydrogen, Admin API) → `/shopify-dev`
   - Next.js / React → `/nextjs-dev`
   - AI / LLM app → `/ai-app-dev`
3. **Scope it**: list the files to change, the smallest sequence of steps, and how it will be verified.
4. **Surface unknowns** as explicit questions rather than guessing.
5. **Output** a short plan: Context → Steps → Files → Verification. Hand off to `/scaffold` (new
   project) or `/implement` (existing code).

If `superpowers` is installed, prefer its brainstorming/planning skills for deep planning and use this
as the CloudKey entry point that routes to the right platform skill.
