<!-- source: https://github.com/can1357/oh-my-pi/blob/main/docs/session-tree-plan.md -->
# Session tree architecture (current)

Not a future plan. How the system works today, with key files and constraints.

## What this subsystem is

Session is an append-only entry log; runtime is a tree.

- Every non-header entry has `id` and `parentId`.
- Active position is `leafId` in `SessionManager`.
- Append always creates a child of the current leaf.
- Branching does **not** rewrite history; it only moves the leaf before the next append.

Key files:

- `src/session/session-manager.ts` — tree, leaf movement, branch extraction
- `src/session/session-context.ts` — reconstruct root→leaf LLM context
- `src/session/agent-session.ts` — `/tree` navigation
- `src/modes/components/tree-selector.ts` — tree UI

## Leaf movement

1. `branch(entryId)` — set leaf; no new entry
2. `resetLeaf()` — leaf = null; next append is a new root
3. `branchWithSummary(...)` — move leaf, append `branch_summary` as child

`/tree` navigates the same session file. `/branch` (default) forks a new session file from a **user** message. Config caveat: `doubleEscapeAction=tree` makes `/branch` same-file navigation.

## Constraints

- `branch()` cannot target `null`; use `resetLeaf()`.
- Selecting the current leaf is a no-op (except interactive `ask` re-answer).
- Summarization needs a model + API key; abort cancels navigation.
- Plan-mode approval seeds the session name from the plan title (`humanizePlanTitle`), only if unnamed.

Design the shape first (a DSL, not a runtime-filled type) so agent-written follow-up stays clean.
