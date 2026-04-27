# AGENTS.md — Cat Fortune V4

## Project Goal
V4 is the final visual/layout iteration of Cat Fortune, based on V3 stable gameplay and PRD 0427 visual requirements.

## Rules for Codex
- Preserve V3 gameplay logic unless explicitly instructed.
- Prefer small, reversible edits.
- Do not modify CSV/runtime data unless the prompt explicitly asks.
- Do not commit or push unless explicitly instructed.
- Use asset-map-0427.json for image paths.
- Do not hardcode fragile image paths directly when avoidable.
- Keep PRD component sizes as visual references, not strict constraints.
- Avoid large rewrites.
- Report modified files and validation results at the end.

## Validation Defaults
For UI-only edits, usually run:
- node -c app.js
- node scripts/validate-assets.js

For data/runtime edits, run:
- node scripts/compile-csv-to-runtime.js
- node scripts/validate-content.js
- node scripts/build-content-report.js
- node -c app.js
