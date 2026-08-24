<!-- source: https://github.com/leerob/pixo/blob/main/.cursor/plans/rust_image_compression_library_3adbb238.plan.md -->
# Cursor plan = spec (todo DAG)

```yaml
name: Rust Image Compression Library
overview: Build a minimal-dependency Rust library … from scratch, with hand-implemented compression and standard test suites.
todos:
  - id: setup-project
    content: Initialize Cargo project …
    status: completed
  - id: png-encoder
    content: Assemble PNG chunks and complete encoder
    status: completed
    dependencies: [png-filtering, deflate-encoder]
```

Then:

```
# Rust Image Compression Library (`comprs`)
## Architecture Overview   # mermaid flowchart, pipelines not packages
## Project Structure       # file tree
```

Ids stay stable. Status lives on the todo. Deps are the order.

Standing `AGENTS.md` beside it: commands (`cargo test`, `cargo fmt && cargo clippy`), architecture map, "changing benchmarks? update BENCHMARKS.md."
