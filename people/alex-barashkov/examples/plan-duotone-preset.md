<!-- source: https://github.com/pixel-point/toolcraft/blob/main/examples/ascii/docs/plans/2026-07-13-duotone-preset-renaming.md -->
# Independent duotone preset naming

## Goal

Replace every name in the duotone preset dropdown with a product-owned label and internal id. Keep exact color pairs and effect behavior.

## Product decisions

- Keep the built-in `select` control, Duotone entity, renderer, randomize, export, ordering.
- Rename `Custom/custom` → `Manual/manual`.
- Replace the eighteen fixed labels with the new product names.
- Preserve every fixed preset's `ink` and `paper` hex.
- No legacy id aliases. Old imported settings may need re-pick. Intentional.
- Timeline, layers, persistence, media, canvas, image export unchanged.

## Files

1. `src/app/effect-presets.ts` — new labels/values
2. `app-schema.ts`, `effect-state.ts`, `panel-actions.ts` — defaults, visibility, randomize
3. Unit coverage for ordered inventory + unchanged color resolution
4. `e2e/app-controls.spec.ts` — current names, reject legacy labels, prove output changes
5. Record in `docs/toolcraft/agent-worklog.md`

## Verification tier

Verification tier: Tier 2

Reason: Visible options, schema defaults, and runtime ids change; renderer/workload/canvas/export do not.

Run: focused unit tests; `npm run verify:quick`; focused browser control-to-output check.

Skip: perf checkpoint (labels are constant-time lookup). Skip `verify:final` (post-first-working scoped pass).
