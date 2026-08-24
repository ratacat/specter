<!-- source: https://github.com/badlogic/pi-mono/blob/main/AGENTS.md -->
# Development Rules (Pi)

Standing spec. Not a feature plan.

## Conversational Style

- Keep answers short. No emojis in commits/issues/PRs/code. No fluff.

## Commands

- After code changes (not docs): `npm run check`. Fix all errors/warnings/infos before committing.
- Never `npm run build` or `npm test` unless asked.
- Never the full vitest suite (e2e fires if env vars present). Use `./test.sh` or a specific file.
- If you create/modify a test, run it until it passes.
- Never commit unless the user asks.

## Git (multi-agent cwd)

Multiple Pi sessions share this tree.

- Only commit files YOU changed in THIS session.
- `git add <path>` — never `git add -A` / `git add .`
- Never: `git reset --hard`, `git checkout .`, `git clean -fd`, `git stash`, `git commit --no-verify`

If rebase conflicts: resolve only files you modified. Else abort and ask.

## Issues and PRs

Don't `gh pr checkout` / switch the worktree onto a PR branch unless asked. Inspect with `gh pr view` / `gh pr diff`.
