<!-- source: https://github.com/ai-that-works/ai-that-works/blob/main/2025-08-05-advanced-context-engineering-for-coding-agents/thoughts/shared/plans/baml-test-assertion-validation-with-research.md -->
# BAML Test Assertion Validation Implementation Plan

## Overview

Fix validation where BAML tests accept `@assert` (field-level) without warnings. Runtime only honors block-level `@@assert`.

## Current State Analysis

- Parser accepts both in `parse_value_expression_block.rs:103-126`
- Test visitor only collects block-level attrs in `configurations.rs:265-275`
- No reject in `validations/tests.rs`
- Prior art: type-alias attribute restrictions in `attributes/mod.rs:217`

## What We're NOT Doing

- Changing parser grammar
- Changing runtime (block-level stays the only evaluator)
- Adding field-level assertions in tests

## Implementation Approach

Add semantic validation to reject `@assert` / `@check` on test fields. Follow type-alias restriction pattern.

## Phase 1: Add Validation for Field Attributes in Tests

**File**: `engine/baml-lib/baml-core/src/validate/validation_pipeline/validations/tests.rs`

```rust
// push DatamodelError if field attr name is assert|check
// message: "@{} is not allowed on test fields. Use @@{} at the test block level instead."
```

### Success Criteria
- [ ] `cargo test test_validation test_field_assertions`
- [ ] `cargo test` / `cargo clippy` green
- [ ] Error points at the invalid attribute; no false positives on `@@assert`

## Phase 2: Add Validation Test Case

**File**: `engine/baml-lib/baml/tests/validation_files/functions_v2/tests/field_level_assertions.baml`

## References

- Research: `thoughts/shared/research/2025-08-05_05-15-59_baml_test_assertions.md`
- Issue #1252
