<!-- sources: https://github.com/kingbootoshi/directional-prompting ; https://github.com/kingbootoshi/rgr -->
# Intent lock, then directional prompt, then RGR

## 1. Lock intent (before any plan)

`intent-contract` → human-signed Locked Intent Boundary:

- required deltas
- invariants
- non-substitutions
- authorized-change rights (every diff op maps to a row)

Compile to a hash-pinned **IntentLock**. `rgr lock-intent --expect-sha256 <H>` stores evidence under `.rgr/`. CI reads a trusted copy the agent does not control.

## 2. Write the directive (outcome + direction)

```
Goal: <one sentence>

Success means:
  - <checkable output 1>
  - <checkable output 2>
  - <format / schema constraint>

Stop when: <explicit stopping condition>
```

Body: lead with the verb of the correct action. "Read the file before answering." not "Don't make assumptions."

## 3. Prove it (`rgr`)

```bash
rgr init --goal-id billing-scope
rgr red --strict --goal-id billing-scope --test src/billing.test.ts -- bun test src/billing.test.ts
rgr green
rgr refactor -- bun test
rgr verify --ci --replay --intent-lock <trusted> --expect-intent-sha256 <H> -- bun test
```

Red must fail. Green refuses if the frozen test bytes changed. Wrong test → `rgr revise-test`, then a new Red. Never quiet-edit the oracle during Green.
