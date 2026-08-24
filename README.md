# Specter

A living house for how AI builders write specs and plans, and how they ship with coding agents.

Specter gathers **parts** of those ways of working: headings, splits, forbids, and ready-made spec/plan shapes you can steal for agent-led software work. It is not a product. It is a kit.

This repo stays **alive**. It pulls from the GitHubs and X accounts of the chosen builders so the notes stay near what they think and ship *now*, not what they said a year ago.

## What you get

- **Parts of specs and plans** — the same kinds of blocks showing up across builders (problem, success, later work, work units, and so on), collapsed into a shared word-list.
- **Ready-made shapes** — a house spec schema you can drop into agent work.
- **Ways of working** — how each builder actually drives agents: when they write a spec, when they skip it, what they lock, what they leave to the model.

## Layout

```
AGENTS.md                 short rules for agents working in this repo
people/
  <builder>/
    person.yaml           GitHub, X, work, and how they work right now
    example.md            one real spec or plan (not a life story)
specs/
  components.yaml         shared words for spec/plan parts
  specfinition.md         house spec shape (what a spec holds)
```

One folder per builder. `person.yaml` is the map. `example.md` is a true sample from their work.

## Shared words

See [`specs/components.yaml`](specs/components.yaml). Those names are the house tongue for spec parts. Infer the product’s own words; do not make up stand-ins.

The house spec shape lives in [`specs/specfinition.md`](specs/specfinition.md).

## Builders

### Alex Barashkov

[X](https://x.com/alex_barashkov) · [GitHub](https://github.com/pixel-point)

Ships one-off design tools instead of living in Figma. Plans are dated lists of product choices, the files they touch, and a **check tier** (how hard you must prove it). A work log is a gate: tests fail if the trail of choices is missing. He would rather spend a day locking math and feel than one-shot a pretty miss.

### Andrej Karpathy

[X](https://x.com/karpathy) · [GitHub](https://github.com/karpathy)

The spec is often a short `program.md` or a long voice ramble, not a book. In autoresearch the human never touches the Python: the agent hacks, trains for five minutes, keeps the run if the score rises, else resets. One dial, one metric, no giant config objects. Give a first paragraph and a token budget; let the model write the rest.

### Andrew Farah

[X](https://x.com/andrewfarah) · [GitHub](https://github.com/afar1)

Context lives on disk, not in chat. Bookmarks become local files an agent can search. New work is born from a **seed** of real bookmarks plus the codebases they must fit, scored on a grid. Each surviving idea ships a copy-paste goal prompt for Claude Code or Codex. Nightly runs are first-class.

### Bootoshi

[X](https://x.com/KingBootoshi) · [GitHub](https://github.com/kingbootoshi)

Every sentence is a **do**, not a don’t. First lock intent (what must change, what must not) and hash it. Then write Goal / Success means / Stop when. Red-green-refactor is evidence: the failing test is frozen; green may not edit it. Claude steers; Codex does the grind in tmux.

### Boris Cherny

[X](https://x.com/bcherny) · [GitHub](https://github.com/bcherny)

Plan mode until the plan is good, then let the agent write. A shared `CLAUDE.md` is the living spec: every miss is written there or into a skill, not patched in chat. Many sessions and worktrees at once. If the model keeps going down a rabbit hole, the bug is in the rules file, not the chat.

### Can Bölük

[X](https://x.com/_can1357) · [GitHub](https://github.com/can1357)

Builds the harness (oh-my-pi), then lives in it. Specs are standing `AGENTS.md` plus a current-state map of the system, not a 50-chapter plan. Shape the work as a small language first; fill it in later. Plan-mode yes/no names the session from the plan title.

### Cole Murray

[X](https://x.com/colemurray) · [GitHub](https://github.com/ColeMurray)

The year of the **background** agent: send a prompt and an environment, shut the lid, read the PR later. Specs are short ADRs (what we chose and why). Docs say how it works now. Secrets never go in the sandbox. Many sessions at once; Linear and GitHub are the inbox.

### Dax

[X](https://x.com/thdxr) · [GitHub](https://github.com/thdxr)

OpenCode tries not to invent a new way for agents to work. Match the tools and flow the model was already trained on; a clever extra loop often scores worse. The repo names its words hard (`CONTEXT.md`) so “system prompt” and “session history” never blur. Small learnings land in the nearest `AGENTS.md`.

### Dex Horthy

[X](https://x.com/dexhorthy) · [GitHub](https://github.com/dexhorthy)

Research (human-read) → plan (human-read) → build. Bad research wastes thousands of lines; bad plans waste hundreds. Keep the spec and the code from becoming a fake twin. Throw out wrong research and start over. Human eyes on research and plan, not the PR.

### Elvis Sun

[X](https://x.com/elvissun) · [GitHub](https://github.com/elvisun)

A week is a loop: plan Friday, heavy agent work on the weekend, close mid-week, launch Thursday. Quality is a **score from a real practitioner**, not a vibe. One news item becomes many angles; each angle gets its own research agent. Turn ops pain into software bugs — those get fixed.

### Jason Kneen

[X](https://x.com/jasonkneen) · [GitHub](https://github.com/jasonkneen)

Lazar is a small locked kernel and one tool (`bash`). Skills on disk are the agent’s self. Plans are numbered files with a drift check, in/out of scope, step-by-step proof, and **STOP** lines. What was looked at and thrown out is written down so the next pass does not re-open it. The human merges.

### Jeffrey Emanuel

[X](https://x.com/doodlestein) · [GitHub](https://github.com/Dicklesworthstone)

Huge iterated plans, then beads (epics, tasks, deps), then a swarm. A short `PLAN_TO_*.md` holds the hard rules; a long book sits beside it. **Running work is the bead graph**, not the book. Clean-room replan (ignore the old code) then rebuild. Anti-ceremony on purpose.

### Josh Pigford

[X](https://x.com/Shpigford) · [GitHub](https://github.com/Shpigford)

Plan mode is not enough — it misses fresh docs. First `/research` (code, docs, web in parallel). Then three files: research, implementation, progress. Each phase must ship something you can try. A **new** context checks the work, and an adversarial pass hunts cheats. One task done fairly beats three done thin.

### Kun Chen

[X](https://x.com/kunchenguid) · [GitHub](https://github.com/kunchenguid)

The spec of a project is `VISION.md`: an accept/refuse policy, not a roadmap. You talk to one Firstmate; it hands work to a crew. Scout means a report, never a PR. Ship means a cloud agent plus a fresh-eyes review. Chat is not the backlog. Scripts do the exact bits; agents do the judgment.

### Lauren

[X](https://x.com/poteto) · [GitHub](https://github.com/poteto)

“The best spec is code.” Plan mode is optional. Walk the subsystem, name the data shape, hand the write to a subagent, **prove it on the real surface** (compile is not done). Smallest change. Subtract before add. Do not block on the human. Parallel only after one agent is trusted.

### Lee Robinson

[X](https://x.com/leerob) · [GitHub](https://github.com/leerob)

Cursor plans are the spec: a todo graph with stable ids, then a map of the system. Standing `AGENTS.md` lists commands and house rules. Now at SpaceXAI, training models for the Bot harness — the cloud harness is the product, not a model picker.

### Mario Zechner

[X](https://x.com/badlogicgames) · [GitHub](https://github.com/badlogic)

No 50-chapter plans. The spec is standing `AGENTS.md` (style, git, tests, never-do) plus issues and PRs. Many Pi sessions share one tree, so git is strict: add only your paths, never `git add -A`, never hard reset. Build the harness (Pi); keep the rules short.

### Matt Pocock

[X](https://x.com/mattpocockuk) · [GitHub](https://github.com/mattpocock)

Locked chain: wayfinder → spec → tickets → implement. Specs name the outcome (problem, solution, long user stories, out of scope) and **do not name files**. Foggy work becomes a map of decision tickets, not a giant plan. After the spec is agreed, the human can walk away; agents fill the tickets.

### Mitchell Hashimoto

[X](https://x.com/mitchellh) · [GitHub](https://github.com/mitchellh)

The human owns the spec. Agents own the hunt for misses. He reads the spec himself; Fable and Sol loop for weeks writing tests that try to break the work, with a judge that assumes ill will. Ghostty forbids outside AI slop; maintainers may use agents, but a human must still understand every line.

### Peter Steinberger

[X](https://x.com/steipete) · [GitHub](https://github.com/steipete)

Do not plan unless asked. Standing law lives in `VISION.md`. Feature work is a dated design spec (choice, accepted behavior, non-goals, required tests) then a TDD plan that names files and failing tests. `AGENTS.md` is scar tissue — every miss that hurt twice gets a line.

### Steve Yegge

[X](https://x.com/Steve_Yegge) · [GitHub](https://github.com/steveyegge)

The spec is not a markdown book. It is **beads**: a graph of work with deps. Agents take `bd ready`. A plan file becomes an epic plus tasks. Git holds what changed; beads hold why. Personal joy is smooshing leftover code with an agent; fleet loops smoosh the rest.

### Thariq Shihipar

[X](https://x.com/trq212) · [GitHub](https://github.com/ThariqS)

HTML is the new markdown. Specs, plans, reviews, and small editors ship as one HTML file with no build. Claude can draw, sort, and change the artifact in place. Skills stay small; put scripts and late-loaded bits inside, not a novel in the skill body.

### Thibault Sottiaux

[X](https://x.com/thsottiaux) · [GitHub](https://github.com/thsottiaux)

Leads Codex at OpenAI. “Scaffolding is coping, not scaling.” A heavy harness that props up a weak model becomes a lid when the model grows. Build the agent first; strip the scaffold over time; let the model do the work. Cache hit rate is how long sessions stay cheap.

### Trevin Chow

[X](https://x.com/trevin) · [GitHub](https://github.com/tmchow)

Compound Engineering: a short `STRATEGY.md` first, then brainstorm → plan → work. The plan is **rails, not a script**: choices, scope, stable U-IDs, files, tests, risks. No exact function names or shell steps — those rot. The worker sees the code and figures how. Thin sections get a second look on their own.

### Trevor I. Lasn

[X](https://x.com/trevorlasn) · [GitHub](https://github.com/trevorlasn)

The product spec *is* the API: REST, local MCP, remote MCP, one `llms-full.txt`. Support tickets are the next-fix spec. Branch per task; throw the branch away if it goes bad. A flow you keep repeating becomes a version-pinned skill file, not a prompt tweak.

## License

This repo’s own words are for learning and reuse in your agent setup. Samples from other folks stay under their own licenses — follow the source links.
