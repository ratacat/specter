<!-- source: https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/eval.md -->
# Eval (`/poteto-mode`)

Different playbook from Feature. You own experiment design: plan, blind, run, synthesize.

## Invariants (blinding)

No `eval`, `test`, `judge`, `experiment`, `rubric`, `score`, `compare`, `benchmark`, `candidate`, or `arena` in any directory, file, or prompt the candidate sees. Organic user request. No chain-eliciting cues. Sanitize slugs. Judge sees sanitized labels, never model names. One judge scores both sets in one pass.

## Work units

1. Frame the variant and a 3–6 criterion rubric (judge only).
2. Set up sanitized environments.
3. Author one organic prompt.
4. Spawn N parallel candidates.
5. Spawn one blinded judge on a different model family.
6. Verify the chain from transcripts and files actually opened, not self-report.
7. Read every candidate output. Synthesize vs the judge.

## Success

Reply names: variant under test, rubric, per-candidate notes, judge verdict, synthesis, promote or not.
