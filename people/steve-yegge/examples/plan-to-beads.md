<!-- source: https://github.com/gastownhall/beads/blob/main/integrations/claude-code/commands/plan-to-beads.md -->
# Convert Plan to Beads Tasks

Plan markdown is input. The live spec is the graph.

1. Find the plan (`# Plan:` / `## Summary` / `### Phase N:`).
2. Epic:

```bash
bd create "[Plan Title]" -t epic -p 1 -d "[summary]. Files: N to modify." --json
```

3. Each phase → task:

```bash
bd create "[Phase title]" -t task -p 2 -d "[first paragraph]" --json
```

4. Sequential deps: `bd dep add <phase2> <phase1>`
5. Link to epic: `bd dep add <epic> <task>`
6. Agents start at `bd ready`.

```
Epic: [title] ([epic-id])
  ├── [Phase 1] ([id]) - ready
  ├── [Phase 2] ([id]) - blocked by [prev]
  └── [Phase 3] ([id]) - blocked by [prev]
```

Original plan file stays as reference. Task descriptions stay one paragraph (scannable).
