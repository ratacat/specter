<!-- source: https://github.com/anomalyco/opencode/blob/dev/packages/opencode/specs/effect/errors.md -->
# Typed Error Migration

A module spec, not CONTEXT.md. Expected failures, service error shape, HTTP boundary.

## Goal

Expected service failures live on the Effect error channel. Domain errors are `Schema.TaggedErrorClass`. `Effect.die` is for defects only. HTTP status and public bodies are handled at route boundaries, not inside service modules.

## Data models

```ts
export class SessionBusyError extends Schema.TaggedErrorClass<SessionBusyError>()("SessionBusyError", {
  sessionID: SessionID,
  message: Schema.String,
}) {}

export type Error = Storage.Error | SessionBusyError
```

Rules: export a domain `Error` union; put expected errors in method signatures; do not `throw` / `Effect.die` for user, IO, validation, missing-resource, auth, provider, worktree, or busy-state failures.

## Architecture

Service modules stay transport-agnostic. HTTP handlers translate service errors into public endpoint errors. User-facing boundaries render structured details, not `Error: SomeName`.
