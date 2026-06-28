---
name: test
description: Phase 4 of the CloudKey SDLC. Run lint, test, and build; report failures verbatim and drive them to green.
---

# Phase 4 — Test

Goal: confirm the work is green, or report exactly what is red.

Run, in order, the project's validation suite:
```
lint   (e.g. npm run lint)
test   (e.g. npm test)
build  (e.g. npm run build)
```

- Report each as PASS or FAIL, with failing output verbatim (assertion, lint rule + location, build error).
- On failure, analyze the actual output, make the smallest fix (or hand back to `/implement`), and re-run all three.
- End with `ALL GREEN` or `RED: <which checks failed>`.

Never claim a check passed without running it. When all three pass, hand off to `/review`.

If the `loop-engineering` plugin is installed, its `tester` agent does exactly this — delegate to it.
