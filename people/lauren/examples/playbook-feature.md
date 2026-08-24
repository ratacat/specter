<!-- source: https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/feature.md -->
### Feature (`/poteto-mode`)

**You own the design. Plan, review, verify.** Delegate implementation; stay in the lead.

1. `/how` over the affected subsystem.
2. `/architect` for parallel design exploration. Skipping stays as `architect skipped: <reason>` — do not fold the design silently into implementation.
3. Throughput checkpoint as four todos (keep `n/a: <reason>` rather than drop):
   - **Blocking first steps.** Gates before fan-out.
   - **Independent workstreams.** Disjoint files/services parallelize; shared writes serialize.
   - **Shared mutable state.** Split the target; serialize only for real invariants.
   - **Smallest safe decomposition.** If one worker is best, name why.
4. Delegate code-writing to a subagent with a specific scope: file paths, named data shape (state machine / table / typed model — chosen before logic), success criteria. Review the diff yourself. Multiple valid shapes → `/arena`. Verify on the matching surface. "Inconclusive" is not a pass.
5. Rebase into small ordered commits. Sequence verifiable units.
6. Contested design → `/interrogate` before shipping.

Reply: what you built, what you chose and why, open decisions. Tables for design alternatives.

pstack README: no bundled planning skill. Cursor plan mode works if you want it. Personally, the best spec is code.
