<!-- source: https://github.com/jasonkneen/tiny-world-builder/blob/main/plans/asset-schema/02-SPEC-tinyworld-asset-1.md -->
# SPEC — `tinyworld-asset/1`

A data-model spec. Declarative JSON for every pure-Three.js asset. Status: DRAFT v2.

## Invariants (design rules)

1. Palette indirection: ops reference palette keys, never raw hex.
2. Sanitize on ingest; unknown keys dropped with warnings.
3. Data describes intent; renderer owns technique.
4. Layers are toggleable overlays.
5. Everything versioned: `format: "tinyworld-asset/1"`. Migration functions, never in-place mutation of old saves.

## Data models

Envelope: `format`, `id`, `name`, `class` (`building | object | foliage | terrain | environment | artifact`), `tags`, `palette`, `params`, `parts`, `voxels`, `layers`, `anchors`.

Geometry blocks: `voxels` (chunky grid), `parts` (primitive ops), `slots` + `sockets` (rigged/attachable), materials via palette + `shader:<id>`.
