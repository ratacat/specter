<!-- source: https://github.com/ai-that-works/ai-that-works/blob/main/2025-08-05-advanced-context-engineering-for-coding-agents/thoughts/shared/plans/fix-assert-syntax-validation-no-research.md -->
# Fix @assert vs @@assert (plan, no research pass)

Same bug as the with-research plan. This file is the **no-research** twin: still Current State, What We're NOT Doing, phases, file paths, success criteria. Used as a paired specimen.

## Overview

`@assert` is accepted in test blocks by the linter and ignored at runtime. Only `@@assert` evaluates. False-positive greens.

## Current system

Grammar: `@attribute` field-level, `@@attribute` block-level. `visit_test_case` only collects block-level constraints. Field-level attributes parse and never validate.

## Out of scope

No grammar change. No runtime evaluator change. No `@@assert` behavior change. No non-test attribute syntax.

## Work units

Phase 1: reject `@assert` / `@check` on fields inside test blocks in `visit_test_case` (`configurations.rs`). Error text must name `@@assert`.

Phase 2: test coverage.

## Success

`cargo test` / `cargo check` / `cargo clippy` pass. VSCode errors on `@assert` in tests. Valid `@@assert` tests still work.
