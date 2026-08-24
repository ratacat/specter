<!-- source: https://github.com/Dicklesworthstone/frankengit/blob/main/docs/ADR-0001-CANONICAL-STATE.md -->
# ADR-0001: Canonical state is an immutable decision stream

An ADR, not a `PLAN_TO_*`. Status proposed (rev 2). Decision owners: FrankenGit architecture.

## Context

Git objects are immutable; forges still treat one mutable POSIX directory as the repo unit. FrankenGit adds a decision stream covering refs and forge events, with one authenticated authority head.

## Decision

1. Canonical bodies are immutable (Git objects, envelopes, seals, forge events, evidence, retention roots). Put-if-absent. Arrival does not establish order.
2. One small `RepositoryAuthorityHead` key establishes canonical order (monotone generation, predecessor, latest batch, ref root).
3. Transaction outcomes are derived from the stream; accelerators are safe caches, not authority.
4. FrankenSQLite is the local authority profile.
5. Everything else is a derived materialization.

## Invariants

Canonical order comes from the authority head, not from directory mtime. Materializations are disposable.

## Rejected alternatives

Mutable bare repo as sole truth. External SQL refs plus a separate WAL as co-authorities. One leased primary writer. Async active-active multi-master refs.
