<!-- source: https://github.com/can1357/oh-my-pi/blob/main/docs/blob-artifact-architecture.md -->
# Blob and artifact storage architecture

Current system, not a future plan. How two stores work today.

## Why two stores

- **Content-addressed blobs** (`blob:sha256:<hash>`): global. Large image payloads. Dedup by hash.
- **Session-scoped artifacts** (files next to the session jsonl): full tool outputs, subagent outputs. Local ids.

Intentional split: blobs outlive a session; artifacts follow one session.

## Boundaries

Blob store is global (`<blobsDir>/<sha256-hex>`). Reference in entries: `blob:sha256:<64 lowercase hex>`. Writes are put-if-absent.

Artifacts live in `<timestamp>_<sessionId>/` beside the jsonl. Types: truncated tool logs (`artifact://`), subagent markdown (`agent://`).

## Data models

Blob ids: content hash. Artifact ids: session-local monotonic integers. Subagents can share the parent's artifact directory and id space.
