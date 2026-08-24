<!-- sources: https://docs.0xinsider.com ; https://github.com/0xinsider/docs.0xinsider.com/blob/main/recipes/insider-scanner.mdx -->
# Agent-facing domain API (0xinsider)

The spec of the product *is* the API. One subscription, three doors:

- REST `https://api.0xinsider.com/api/v1/`
- Local MCP `@0xinsider/mcp` (stdio)
- Remote MCP (Streamable HTTP)

Agents start at [llms-full.txt](https://docs.0xinsider.com/llms-full.txt) and the unauthenticated discovery route (complete `authenticated_routes` index, not a sample).

## Domain language (stable objects)

Trader grades `S`–`F`. `trd_` / `flg_` IDs. Whale trades, positions, insider radar (`suspicion_score`, `severity: flag|watch`, component scores `timing|edge|size|fresh_wallet`). Trust metadata on values. Cursor pagination. `expand` for optional strategy/quant/trust fields.

## Recipe = procedure spec

Insider scanner (`recipes/insider-scanner.mdx`):

1. Pull flags (`severity=watch`, `min_suspicion=70`)
2. Open one flag
3. Confirm with trader + market intel — "a flag is a lead, not proof"
4. Cross-check size via large-positions

Each step is a real route, not a vibe. Changelog.mdx is required follow-through for any externally visible API change, same branch.

## How he implements (X, 2026)

Support tickets → next-fix specs. Branch per task (copy-on-write); destructive work stays on the branch. Repeated workflow → version-pinned skill file, not a prompt edit.
