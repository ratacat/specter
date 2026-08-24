<!-- source: https://github.com/Dicklesworthstone/fastmcp_rust/blob/main/PLAN_TO_PORT_FASTMCP_TO_RUST.md -->
# Plan To Port FastMCP To Rust

Short-form PLAN_TO_*. Comprehensive books (FrankenGit 52 chapters) sit beside this.

## Non-Negotiables

- **Protocol correctness**: stdout is NDJSON JSON-RPC only. Human output → stderr.
- **Cancel-correctness**: cooperative cancellation via `asupersync`.
- **Unsafe is forbidden**: `#![forbid(unsafe_code)]`.
- **Minimal dependencies**: pin versions in Cargo.toml.

## Source Of Truth

1. `EXISTING_FASTMCP_STRUCTURE.md` (the spec)
2. `PROPOSED_RUST_ARCHITECTURE.md` (how Rust implements it)
3. `FEATURE_PARITY.md` (parity checklist)

Python is reference for edge cases only.

## Work Breakdown (Phases)

### Phase 1: Protocol + Types

- JSON-RPC framing; MCP domain types; serde

Acceptance: round-trip serde tests; schema tests; fixtures.

### Phase 2: Transport Layer

Acceptance: transport conformance tests.

### Phase N: …

Acceptance: named testable criterion.

## Quality Gates (Always)

```bash
cargo fmt --check
cargo check --all-targets
cargo clippy --all-targets -- -D warnings
cargo test --all --all-targets
```
