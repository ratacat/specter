<!-- source: https://github.com/pixel-point/toolcraft/blob/main/examples/bricks/docs/superpowers/specs/2026-06-24-brick-mosaic-design.md -->
# Brick Mosaic Design

A destination spec, not the later implementation plan. Product goal, behavior, control inventory, renderer decisions, then acceptance.

## Product Goal

One uploaded image, rendered as a grid of raised toy-brick tiles. User tunes brick style, sampling, monochrome, tone, and PNG export.

## Product Behavior

- Upload through built-in `fileDrop`. Canvas uses `intrinsic-media` sizing.
- Preview and export are the same Canvas 2D mosaic, not app UI.
- No image: still draw a neutral brick preview so controls have output.
- No timeline (still output). No layers (one source, one result).
- Settings persist; media blobs do not.

## Inventories (not a file tree)

Control sections: Source Image, Brick Grid, Studs, Tone, Lighting, Background, Image Export. Each names the schema keys it owns.

Control selection: for each control, value model, built-ins checked, best built-in, target key, what acceptance must prove.

Renderer matrix: `image-media` source, `canvas-2d` preview and export, why not DOM/SVG/WebGL.

Renderer layers: `backgroundLayer`, `productForegroundLayer`, `exportComposite`.

## Acceptance

Verification tier: Tier 4. Run `pnpm verify:final`, `pnpm verify:perf`, then `pnpm dev`.
