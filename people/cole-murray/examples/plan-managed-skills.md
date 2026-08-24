<!-- source: https://github.com/ColeMurray/background-agents/blob/main/docs/plans/managed-skills.md -->
# Managed Skills

A proposed design (plan), not an ADR. Four named concepts, a decision table, current architecture, goals, non-goals.

## Domain language

- **Skill** — installation-wide Agent Skills package
- **Assignment** — global / repo / environment applicability
- **Profile** — a user's selection from applicable skills
- **Session manifest** — immutable revisions pinned to one session

Editing a skill does not mutate running sessions.

## Design decisions (table)

Format: portable `SKILL.md` directory. Resolve then pin at session create. D1 metadata for V1. Sandbox-authenticated manifest; no skill content in env vars. Fail sandbox startup if install fails. Immutable internal revisions; user-facing history deferred.

## Current system

Admission is one-tenant. Environments snapshot repos into `session_repositories`. Safe insertion: after repo boot, before `opencode serve`.

## Out of scope (V1)

Multi-team ACL, marketplace, Git sync, user-facing version history, binaries, skill dependencies, updating a live session, evals/canaries, hosts other than OpenCode.
