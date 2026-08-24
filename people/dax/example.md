<!-- sources: https://github.com/anomalyco/opencode/blob/dev/CONTEXT.md ; https://github.com/anomalyco/opencode/blob/dev/.opencode/command/learn.md -->
# Domain language first (`CONTEXT.md`)

Each term is defined, then a forbidden synonym:

```
System Context     — structured facts as initial instructions + chronological updates
  Avoid: System prompt
Session History    — projected conversation after compaction / Context Epoch cutoffs
  Avoid: Session Context
Context Source     — one independently observed typed value in System Context
  Avoid: Prompt fragment
Context Epoch      — span where one rendered System Context is the immutable cache baseline
Admitted Prompt    — durable user input in the inbox, not yet in Session History
Prompt Promotion   — inbox → Session History
Provider Turn      — one request/response to a model provider
Session Drain      — process-local span; no durable identity
```

AGENTS.md then binds implementation: one explicit `llm.stream(request)` per provider turn; durable prompt admission separate from model execution; no `SessionPrompt.loop`. Style: one function unless reusable; no single-use helpers; no `any`; Bun APIs; no aliased/star imports.

## `/learn`

After a session: extract **non-obvious** learnings into the nearest `AGENTS.md` (root / package / feature). 1–3 lines. Not README facts. Not session gossip.
