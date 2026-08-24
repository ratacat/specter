<!-- source: https://github.com/EveryInc/compound-engineering-plugin/blob/main/docs/skills/ce-plan.md -->
# `ce-plan`

Plans capture the WHAT. The implementer (`ce-work`) figures the HOW.

```
/ce-ideate → /ce-brainstorm → /ce-plan → /ce-work
"worth exploring?"  "what is it?"   "what's needed?"  "build it."
```

Also: `/ce-strategy` → `STRATEGY.md` (every CE skill reads this).

## Guardrails, not choreography

The plan records: decisions + rationale, in/out of scope, atomic units, files each unit touches, test scenarios, risks.

It does **not** pre-write code, exact API signatures, or step-by-step shell. Those go stale.

Units are `### U1. Name` — IDs never renumber. Splits keep the original U-ID; deletes leave gaps. `ce-work` cites U-IDs.

When sourced from brainstorm: R-IDs / A-IDs / F-IDs / AE-IDs flow through. Test scenarios cite `Covers AE3`.

After write: confidence check dispatches sub-agents on weak sections and synthesizes back.

## Output contract (picked before research)

- **Direct** — few sentences, hand off to `ce-work`
- **Chat brief** — bounded, one decision, stays in chat
- **Durable** — `docs/plans/YYYY-MM-DD-HHMM-<type>-<name>-plan.md`

Auth/payments/migrations/external contracts are always Durable.

## Recent handoff (2026-08)

Fable: `ce-brainstorm` + `ce-plan`, commit the plan.  
`ce-handoff` → Codex Sol orchestrates; Luna High subagents run `ce-work`. Surface key decisions in the orchestrator. Don't let subagents stall.
