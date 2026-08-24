<!-- source: https://github.com/leerob/pixo/blob/main/.cursor/plans/rust_code_review_5027f498.plan.md -->
# Cursor plan = code review (todo DAG)

Same plan format as the from-scratch library plan. This one is a review of existing Rust, not a greenfield spec.

```yaml
name: Rust Code Review
overview: #[must_use], builders, type aliases, named constants, safety docs, unused params
todos:
  - id: must-use
  - id: builders
  - id: type-aliases
  - id: named-constants
  - id: unused-params
```

Each todo names files (`src/lib.rs`, `src/resize.rs`) and shows the snippet that *is* the decision (`#[must_use] pub fn encode_png(...)`).
