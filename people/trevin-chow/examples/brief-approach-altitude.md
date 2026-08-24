<!-- source: https://github.com/EveryInc/compound-engineering-plugin/blob/main/docs/brainstorms/2026-06-04-ce-plan-approach-altitude-requirements.md -->
# ce-plan approach altitude (requirements brief)

A brainstorm/requirements doc, not the `ce-plan` skill itself. Plan-for-a-plan as a first-class shape.

## Problem

Users ask for an intermediate plan (how you will read the book and the transcript) and then the real deliverable later. Today's classifier is binary: plan-seeking or answer-seeking. The second phase is homeless (`ce-work` is code-only). Ungrounded approach-plans are generic methodology.

## Design decisions

- Boundary is code vs knowledge-work, not plan vs execute. `ce-plan` never executes.
- High-precision / low-recall proactive offer. Named enemy: asking "want me to plan the approach first?" every turn.
- `ce-work` gets a non-code carve-out. Approach-plan is portable.
- Light recon only after the user accepts.

## Actors

User, `ce-plan`, `ce-work` (or any agent for non-code).

## Out of scope

Do not unify this with answer-seeking's plan-of-attack, Phase 0.7 scoping, or the deepening pass. Separate surface, crisp firing rules.
