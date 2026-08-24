<!-- source: https://github.com/afar1/fieldtheory-cli/blob/main/.claude/commands/fieldtheory.md -->
# `ft possible` — bookmark-grounded goal prompts

A spec starts as three things, not a blank prompt:

- **seed** = a group of *actual* X bookmarks (never `ft seeds text`)
- **repos** = codebases the idea must apply to
- **frame** = the 2×2 axes (leverage × specificity, impact × effort, …)

Those make a **run**. Pipeline per repo: `survey → generate → critique → score`. Survivors become **nodes** (dots on the grid):

- title + paragraph
- why adjacent
- axis A/B scores + justifications
- effort (hours / days / weeks)
- a **copiable goal prompt** for any coding agent

```bash
ft seeds search "agents" --days 90 --limit 8 --frame leverage-specificity --create
ft possible run --seed <id> --repos ~/dev/a ~/dev/b --depth quick --nodes 7
ft possible grid latest
ft possible prompt <node-id>    # paste into Claude Code / Codex
```

Depth: `quick ~3–5 min` / `standard ~8–12` / `deep ~20+`. `--background` + `ft possible jobs` for overnight. `--defaults` re-runs the last seed/repos/frame.

On disk (`~/.fieldtheory/ideas/`):

```
seeds|runs|nodes|batches/<YYYY-MM-DD>/*.md
```

YAML frontmatter cross-links (`related_run_ids`, `related_node_ids`, `related_seed_ids`). The Library/Mac app reads the same files. Seeds stay bookmark-grounded; text-only seeds are a footgun.
