---
name: design
description: Design UI/UX before or alongside implementation — translate Figma designs to code, push code to Figma, and apply web interface best practices. Fits between /plan and /implement.
---

# Design (UI/UX)

Use when a CloudKey task involves visual UI: building a screen/component, implementing a Figma design,
establishing a design system, or reviewing an interface. Runs between `/plan` and `/implement`.

## Figma ↔ code (use the connected Figma MCP)
The Figma MCP server is the bridge — do not hand-roll design parsing.
- **Design → code**: given a figma.com frame URL, read it with `get_design_context` / `get_screenshot`
  / `get_variable_defs`, then implement faithfully. Honor design tokens and existing components.
- **Code → Figma**: push a built UI to the canvas as editable frames with `use_figma` (read its
  `/figma-use` skill first, as the MCP requires).
- **Design system**: build/extend a token + component library; map components with Code Connect.

## Web interface best practices (apply to every UI)
Check the work against these before handing to `/implement` or `/review`:
- **Accessibility**: semantic HTML, labelled controls, focus states, keyboard nav, color contrast,
  `prefers-reduced-motion`, alt text.
- **Responsiveness**: mobile-first, fluid layout, no fixed widths that overflow, sensible breakpoints.
- **Performance/UX**: avoid layout shift, optimize images, loading/empty/error states for async data,
  perceptible affordances, consistent spacing scale.
- **Composition**: compound components + context over boolean-prop proliferation; explicit variants.

## Routing
- **shadcn/ui components** (React/Next.js): use the connected `shadcn` MCP to browse the registry and
  add components (e.g. "add the button/dialog component"). Requires a shadcn-initialized project
  (`npx shadcn@latest init`, which creates `components.json`).
- Component/design-system specifics for a platform → defer to `/shopify-dev` (Polaris) or `/nextjs-dev`.
- Verify any framework/styling API (Tailwind, CSS APIs, a UI lib) against live docs via `find-docs`.
- For a focused interface critique, delegate to the `design-reviewer` agent.

Output: the implemented or specified UI plus a short note on which best-practice checks it satisfies.
