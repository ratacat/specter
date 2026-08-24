<!-- source: https://github.com/jasonkneen/lazar/blob/main/plans/012-shell-guard-alignment.md -->
# Numbered plan + STOP conditions (lazar)

Batch from the improve skill against a pinned commit. Index in `plans/README.md` (priority, effort, depends-on, status). Executor: read fully, honor STOP, update the row.

```
# Plan 012: {title}

> Executor instructions …
> Drift check (run first): `git diff --stat <pin>..HEAD -- {files}`
> On mismatch, STOP.

## Status
Priority / Effort / Risk / Depends on / Category / Planned at commit

## Why this matters
{numbered problems; what this is deliberately NOT}

## Current state
{excerpts with file:line, not paraphrase}

## Commands you will need
| Purpose | Command | Expected on success |

## Scope
**In scope**: {paths, and which part}
**Out of scope**: {named; with why}

## Git workflow
Branch, commit message. Do NOT push/PR unless asked.

## Steps
### Step N: {one change}
{exact replacement}
**Verify**: {command} → {exit code / output}

## Test plan
{per-step verifies are the tests; don't invent a harness}

## Done criteria
- [ ] {command → expected}
- [ ] {grep counts}
- [ ] `plans/README.md` status row updated

## STOP conditions
- {unsafe verify}
- {behavior that must not change}

## Maintenance notes
{when a fifth copy appears, then extract a helper — not now}
```

`plans/README.md` also lists **Findings considered and rejected** so the next audit doesn't reopen them. Execution: worktree-isolated subagents; nothing merged until the operator runs a listed merge script + test suite.
