<!-- sources: https://github.com/Shpigford/nurb/blob/main/docs/evals/RESEARCH.md ; https://github.com/Shpigford/nurb/blob/main/docs/evals/IMPLEMENTATION.md ; https://github.com/Shpigford/nurb/blob/main/docs/evals/PROGRESS.md -->
# `/build` — three files, then phases

Live run: nurb LLM eval suite. `/research` first (Plan mode is not thorough enough). Then `/build research|implementation|progress|phase N`.

## `docs/{name}/RESEARCH.md`

```
# {Feature} Research
## Overview
## Problem Statement
## Recommended Approach
## Cost model (the binding constraint)
## Key Codebase Facts          # file:line, APIs that exist vs CLAUDE.md lies
## Prior Art (what the design steals)
## {Named principle, dated}    # decided after a later phase, written back
## Risks and Challenges
## Open Questions
## References
```

nurb: parallel subagents (codebase, CAD-benchmark prior art, harness tooling); load-bearing claims adversarially checked against live docs. Corpus Design Principle written 2026-08-02 *after* phase 3 proved spec-tasks don't separate models.

## `docs/{name}/IMPLEMENTATION.md`

Vertical slice first. Each phase:

```
## Phase N: {shippable result}
### Objective
### Rationale
### Tasks          # checkboxes, concrete files
### Success Criteria   # commands + expected numbers
### Files Likely Affected
```

"Deliver something functional and testable. Never stack multiple infrastructure-only phases." Task design that is decided stays in the plan: "decided here, not re-litigated per file." A later phase may replace an earlier one in place (Phase 2: "Subscription-CLI runner replaces the original Inspect AI plan").

## `docs/{name}/PROGRESS.md`

```
## Status: Phase N Complete …
## Quick Reference  → RESEARCH.md, IMPLEMENTATION.md
### Phase N
**Status:** Complete
**Verified:** Yes — fresh-context verifier passed criteria 1–N independently
#### Tasks Completed
#### Evidence          # exact pytest counts, scores, wall times
#### Decisions Made    # including plan deviations
#### Blockers
#### Review Hardening  # adversarial cheats found, tests added
```

Verifier is a *new* context, not the implementer. Adversarial pass is required: nurb found a closed-tunnel clip scoring 1.0; fixed; cheat kept as `tests/solutions/roofed.py`.
