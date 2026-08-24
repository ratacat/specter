<!-- sources: https://linearb.io/blog/openai-codex-thibault-sottiaux-agentic-autonomy ; https://linearb.io/dev-interrupted/podcast/openai-codex-thibault-sottiaux-agentic-autonomy -->
# Scaffolding is coping, not scaling

Codex design rule: if you need a pile of harness to make the agent work, you are coping with a weak model. When the next capability jump lands, that harness becomes **capability overhang** — it blocks the model from using what it can already do.

## Spec of the agent (not a feature plan)

```
Build the agent first.
Discover scalable primitives (not clever one-off tricks).
Minimize scaffolding. The harness is meant to be removed over time.
Let the model do the work.
```

"It's called a harness because you're scaffolding it in a way where you want to remove the scaffold over time."

## What that forbids

- Vertical integration of clever prompt tricks that won't survive a model bump
- Constraints in the wrapper that the model has outgrown
- Treating syntax/choreography as the product

## Efficiency as spec

Long sessions: **cache hit rate** is how usage stays honest. Compaction + images + hidden title-generation were 2026-08 drains. Measure those; don't paper over them with a bigger quota.

Supported surface: Sign in with ChatGPT on official clients or OSS (Pi, OpenCode). Subscription-to-API resell is out of spec.
