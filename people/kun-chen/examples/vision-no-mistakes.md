<!-- source: https://github.com/kunchenguid/no-mistakes/blob/main/VISION.md -->
# no-mistakes VISION.md (filled)

The `/vision` skill is the template. This file is a finished acceptance policy a later reader applies to a PR.

## Problem

One deliberate push should mean the change was independently validated before anyone else sees it. The tool owns the gate between a local branch and the configured push target.

## Invariants

- One gate, one meaning. Opt-in named remote. Never rewire `origin`. A pass cannot be quietly weakened.
- Never lose work. Force is never blind. Failed verification fails closed.
- Judgment stays human. Mechanics do not. Automation of judgment only by explicit opt-in.
- Independent, adversarial validation in a fresh context. Reviewer and fixer are separate memory.
- Evidence over confidence. Verdicts are traceable and attributable.
- Humans and agents are both first-class users. Same approval semantics.

## Out of scope

Not CI, not an agent orchestrator, not a code host, not team governance. CI stays the shared outer gate.
