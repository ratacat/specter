<!-- source: https://github.com/openclaw/openclaw/blob/main/VISION.md -->
# OpenClaw Vision

Product vision, not the camsnap CLI spec. Current state and direction.

## Goal

A personal assistant that runs on your devices, in your channels, with your rules. Easy to use, many platforms, privacy and security.

## Later work vs now

Now: security and safe defaults, bug fixes, setup reliability, first-run UX.

Next: all major model providers, major messaging channels, performance and tests, computer-use, CLI/web ergonomics, companion apps.

## Invariants

One PR = one topic. PRs over ~5,000 lines only in exceptional cases. Runtime reads the current config schema only; no long-lived aliases. Config breaks get a `openclaw doctor --fix` migration.

## Out of scope (for now)

Named under "What We Will Not Merge."
