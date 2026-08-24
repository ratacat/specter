<!-- sources: https://x.com/bcherny/status/2017742741636321619 ; https://getpushtoprod.substack.com/p/how-the-creator-of-claude-code-actually -->
# Plan mode, then CLAUDE.md is the spec

Personal CLAUDE.md is two lines pointing at the team's. The living spec is shared and committed.

## Session shape

1. **Plan mode** (Shift+Tab twice) until the plan is good. "A good plan is really important."
2. Switch to auto-accept. Usually one-shots the PR from that plan.
3. Parallel: many Claude sessions / worktrees at once.

## Compounding (the only durable spec)

Anytime Claude is wrong: do not tell it "do it differently" in chat. Tell it to **write the rule** into `CLAUDE.md` or a skill.

Chat correction = this run. File = every future run.

During review, tag `@.claude` on a coworker's PR to add the rule in the same PR (GitHub action).

Sticky misses: one **verifier agent per rule**, plus a skeptic that rejects rules that wouldn't have prevented a real mistake.

## Team CLAUDE.md skeleton (from the public tips)

```
# Development Workflow
Always use bun, not npm.

1. Make changes
2. bun run typecheck
3. bun run test -- -t "test name"   # or test:file glob
4. bun run lint:file -- "file.ts"
5. Before PR: bun run lint:claude && bun run test
```

Ruthlessly iterate until the mistake rate drops.
