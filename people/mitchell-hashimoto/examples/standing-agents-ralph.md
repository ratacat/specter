<!-- sources: https://github.com/ghostty-org/ghostty/blob/main/AGENTS.md ; https://x.com/mitchellh/status/2090893729469268109 -->
# Spec is human; tests are a ralph loop

Ghostty Kitty Graphics (2026-08): he read the spec and Kitty source. Agents did not write the protocol. They hunted mismatches.

## Standing rules (`AGENTS.md`)

- `zig build` / `zig build test -Dtest-filter=<name>` (full suite is slow)
- Never create an issue or PR. If asked, write a file that says so.

`AI_POLICY.md`: disclose the tool; human-in-the-loop must explain the change without AI; no AI media. Maintainers exempt.

## Validation factory (the actual plan)

```
1. Sol writes the harness (Kitty GUI + Ghostty GUI, pty stream + screenshots).
2. Fable + Sol (two folders) ralph-loop test cases onto disk.
3. Roles reverse: adversarial judge. Prompt: "Do not trust the author. Assume ill intent."
   Keep only cases that are accurate/worthwhile → third folder.
4. Sol dedupes into the final repo.
Human picks up bug reports, fixes himself or kicks Codex/Claude manually.
Re-run both agents on the full suite. pty asserts byte equality with Kitty.
Screenshots: LLM "do they look the same" + he looked at every one.
```

He will open-source the suite with the disclaimer it is 100% AI-written — "a perfect example of something that SHOULD be."
