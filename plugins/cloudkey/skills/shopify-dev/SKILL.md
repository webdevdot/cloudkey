---
name: shopify-dev
description: Shopify development across themes (Liquid), Hydrogen storefronts, Admin/Storefront GraphQL, Functions, and app extensions.
---

# Shopify development

Use for any Shopify work referenced in a CloudKey phase.

Routing — pick the right surface, then defer to the installed Shopify skills for authoritative API detail:
- **Theme / Liquid** (sections, blocks, snippets, schemas) → `shopify-liquid`
- **Hydrogen** storefront → `shopify-hydrogen` (never use Storefront GraphQL when Hydrogen is involved)
- **Admin API** (products, inventory, orders) → `shopify-admin`; to run against a real store → `shopify-admin-execution`
- **Storefront GraphQL** (custom storefront) → `shopify-storefront-graphql`
- **Functions** (discounts, checkout, delivery) → `shopify-functions`
- **Metafields / Metaobjects** → `shopify-custom-data` (use first when custom data is mentioned)
- **Admin/Checkout/POS UI extensions** → the matching `shopify-polaris-*` / `shopify-pos-ui` skill
- **Scaffolding** a new app/theme/extension → Shopify CLI (`shopify app|theme init`), see `shopify-onboarding-dev`

## Verify against live schema (bundled MCP)
CloudKey bundles the official **Shopify Dev MCP** (`@shopify/dev-mcp`, read-only, no auth). Use it to
introspect the current Admin/Storefront GraphQL schema and search Shopify docs before writing queries —
never rely on memory for GraphQL fields. If the `shopify-plugin` is installed, its API-specific skills
(`shopify-admin`, `shopify-liquid`, …) are the authoritative source; this skill routes to them.
For non-Shopify libraries used alongside (e.g. a frontend lib), use Context7 via `find-docs`.
