<!-- source: https://github.com/ColeMurray/background-agents/blob/main/docs/adr/0001-single-provider-scm-boundaries.md -->
# ADR 0001: Single-Provider SCM Deployment and Boundary Rules

## Status

Accepted

## Context

Open-Inspect runs GitHub as the only production SCM. Contributors want Bitbucket. A `SourceControlProvider` abstraction exists, but GitHub details can leak into non-provider layers.

Keep deployments single-provider. Preserve GitHub. Block unsafe coupling.

## Decision

1. **Single provider per deployment** — `SCM_PROVIDER` selects it. No per-session provider state.
2. **Fail fast** — unimplemented providers (`bitbucket`) → `501` on non-public routes.
3. **Provider/auth boundary** — PR URLs, push transport, sandbox credential helpers live in provider implementations. GitHub API base URL only in approved auth/provider modules.
4. **Guardrails** — code review + focused provider/factory tests.

## Consequences

Positive: no schema expansion; GitHub paths stay auditable; clear insertion point.

Negative: multi-provider-per-deployment unsupported. That needs a new ADR.

## Follow-up

- New provider under `packages/control-plane/src/source-control/providers`
- Register in factory and env resolver
- No provider URL/token logic in router/session/slack
- `generateCredentialHelperAuth` before helper-backed sandbox git auth

The development model around this: send a prompt to a background session, close the laptop, review the PR later.
