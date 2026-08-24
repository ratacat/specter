<!-- source: https://github.com/mattpocock/skills/blob/main/skills/engineering/to-tickets/SKILL.md -->
# to-tickets (Matt Pocock)

Break a spec or conversation into tracer-bullet tickets with blocking edges. Not `to-spec`.

## Work units

Vertical slices: complete path through every layer, demoable alone, one fresh context window. Blocking edges declared. Wide refactors are expand–contract, not tracer bullets.

## Call contract (ticket shape)

```
# <NN>: <Ticket title>
**What to build:** end-to-end behaviour from the user's side
**Blocked by:** ids/titles, or None
**Status:** ready-for-agent
- [ ] Acceptance criterion
```

Quiz the user on granularity and edges, then publish. Local files under `.scratch/<feature-slug>/issues/` or native tracker blocking links. Work the frontier (blockers done). Do not close the parent issue.
