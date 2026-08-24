# Specter

Specter tracks how AI builders write specs and plans, and how they ship with coding agents.

Specter gathers the spec and plan parts those builders actually use: problem, success, design decisions, work units, later work, call contract, and the rest listed below. It also keeps ready-made spec and plan schemas you can drop into agent-led software work. This is not a product.

This repo stays current. It pulls from the GitHubs and X accounts of the builders below so the notes match what they think and ship now, not what they said a year ago.

## Spec parts

These are the named parts Specter uses. Full wording, synonyms, and how an agent should treat each one: [`specs/components.yaml`](specs/components.yaml).

| Part | What it is |
| --- | --- |
| **front matter** | title, date, status, slug, parent |
| **problem** | pain today, from the user's side |
| **current system** | how it works now |
| **solution** | what becomes true when the work is done |
| **user stories** | actor, capability, benefit |
| **success** | checkable facts that the work is done |
| **out of scope** | named no's for this spec |
| **later work** | wanted, not this spec; do not build; let it shape the design |
| **edit whitelist** | domain surfaces this spec may change |
| **edit blacklist** | domain surfaces this spec must not change |
| **invariants** | true before, during, and after |
| **design decisions** | contested calls, and why not the other thing |
| **open questions** | left unset on purpose |
| **call contract** | named verbs a caller runs (CLI, routes, flags) |
| **data models** | durable shapes and meaning |
| **architecture** | modules, interfaces, seams, edges |
| **domain language** | product words already in use; do not invent stand-ins |
| **automation metric** | one number the agent may move |
| **automation budget** | cap that ends a trial |
| **risks** | what might go wrong in this change |
| **work units** | named behaviors this spec must deliver (stable ids) |

## If you just want the spec shape

If you do not want to wade through every builder, and you just want **ratacat's spec definition** after looking at how all of them do it, start here:

**[`specs/specfinition.md`](specs/specfinition.md)**

That file is the preset: what a spec holds, in what order, and what it must not name (no file paths, no function names, no code dumps).

## Layout

```
AGENTS.md                 short rules for agents in this repo
people/
  <builder>/
    person.yaml           GitHub, X, projects, and how they work now
    example.md            one real spec or plan (not a bio)
specs/
  components.yaml         the spec parts above
  specfinition.md         ratacat's spec definition
```

One folder per builder. `person.yaml` is the map. `example.md` is a real sample from their work.

## Builders

### Alex Barashkov

[X](https://x.com/alex_barashkov) · [GitHub](https://github.com/pixel-point)

**toolcraft** (2026-07/08): preflight `workflow.md`, then brainstorm spec, then `writing-plans`, then implement. Figma MCP is the source of truth, not screenshots. Dated plans list product choices, exact files, and a verification tier 0 to 4. `npm run test` fails if the work log (the trail of choices) is missing. 2026-08: does not one-shot; a day of passes to lock math and refs. Grok 4.6 for cheap speed; Fable for design asks.

### Andrej Karpathy

[X](https://x.com/karpathy) · [GitHub](https://github.com/karpathy)

**autoresearch** (2026): the human edits `program.md`, never `train.py`. Loop: hack train.py, train 5 minutes, keep if `val_bpb` improves, else `git reset`. Never stop until cut off. 2026-07: a 10 minute voice ramble *is* the spec; the model writes it clean. 2026-08: first paragraph plus a $10 / 1M-token budget, let Opus write thousands of lines. **nanochat** README is the product spec: one `--depth` dial, no giant config objects, metric is time-to-GPT-2 / CORE.

### Andrew Farah

[X](https://x.com/andrewfarah) · [GitHub](https://github.com/afar1)

**Field Theory CLI**: `ft sync` dumps X bookmarks to disk so any agent with a shell can search them. New work is `ft possible`: a seed of *real* bookmarks (never invented text) + repos + a 2x2 frame (leverage x specificity). Pipeline per repo: survey, generate, critique, score. Each surviving node has a copy-paste goal prompt for Claude Code or Codex. Artifacts are dated markdown under `~/.fieldtheory/ideas/` with YAML links. Nightly / background runs are first-class.

### Bootoshi

[X](https://x.com/KingBootoshi) · [GitHub](https://github.com/kingbootoshi)

**directional-prompting**: Goal / Success means / Stop when. Every sentence is a positive verb; "don't" is a smell. **rgr** (2026): `intent-contract` first (human-signed Locked Intent Boundary: required deltas, invariants, authorized-change rows), hash-pinned IntentLock. Red freezes the failing test (SHA-256); green cannot edit those bytes; `rgr verify --ci --replay` in CI. `.rgr/` is evidence, not authority. 2026-08: Claude orchestrates, Codex in tmux does mechanical work; Cartographer first on unknown repos.

### Boris Cherny

[X](https://x.com/bcherny) · [GitHub](https://github.com/bcherny)

Claude Code (2026 thread + 2026-08 posts). Most sessions start in **Plan mode** (Shift+Tab twice) until the plan is good, then auto-accept; the PR often one-shots from that plan. Team `CLAUDE.md` is git-checked and edited several times a week: every miss is written there or into a skill, not patched in chat. Review: tag `@.claude` on a coworker's PR to add the rule. Sticky misses get one verifier agent per rule. 2026-08: `claude --safe-mode` to tell if the rabbit hole is in CLAUDE.md / skills. Many worktrees in parallel; a loop to wipe stale ones.

### Can Bölük

[X](https://x.com/_can1357) · [GitHub](https://github.com/can1357)

**oh-my-pi** (`omp`). Specs are standing `AGENTS.md` (Bun over Node, no prompt-strings-in-code, contract tests not source-greps) plus current-state architecture docs such as `docs/session-tree-plan.md`. Plan-mode approval names the session from the plan title. 2026-08-17: omp2 is cleaner because the shape was a DSL designed up front, not a TypeScript type filled at runtime. Advisors are agent-definition frontmatter (`/agents`), not a global `/plan`. Channel transference (`/branch` on the session tree) is not Cursor `/plan`.

### Cole Murray

[X](https://x.com/colemurray) · [GitHub](https://github.com/ColeMurray)

**OpenInspect / background-agents** (2026-08-24): "2025 caffeinate flows are dead." Spec is a prompt plus environment (repos, secrets, skills). Execution is a cloud session you check later. Parallel sessions, fire-and-forget PRs, Linear / Slack / GitHub as the inbox. Control plane (Cloudflare Workers, Durable Objects, D1) vs data plane (sandboxes). Secrets stay out of the sandbox (placeholder env + egress proxy allowlist). Decisions as short ADRs (example: single-provider SCM). Docs are current-state how-it-works, not a product book.

### Dax

[X](https://x.com/thdxr) · [GitHub](https://github.com/thdxr)

**OpenCode** at anomalyco. 2026-08-22: "We try not to have too many opinions in how agents should work. Every model is intensely trained to use certain tools and workflows so we try to match that environment perfectly." `CONTEXT.md` is the domain language (System Context vs Session History vs Context Epoch; forbidden synonyms listed). `AGENTS.md` binds implementation (one `llm.stream` per provider turn; durable prompt admission separate from model execution). `/learn` writes non-obvious session findings into the nearest `AGENTS.md` (1 to 3 lines). UI or core product features need design review before a PR.

### Dex Horthy

[X](https://x.com/dexhorthy) · [GitHub](https://github.com/dexhorthy)

**Advanced context engineering** (HumanLayer). 2026-08-19: keeping all specs in sync with all code is a manufactured problem. Pipeline: research doc (human-reviewed) -> implementation plan (human-reviewed) -> implement. Bad research times thousands of bad lines; bad plan times hundreds. Human attention on research and plan, not the PR. Context use about 40 to 60 percent. Throw out wrong research and redo. Plans name files and include test commands. HumanLayer turns underspecified work into something an agent can oneshot; it is not a ticket factory.

### Elvis Sun

[X](https://x.com/elvissun) · [GitHub](https://github.com/elvisun)

**newsjack** + Medialyst (2026-08 7-day sprint). Fri plan/scope; Sat/Sun 4 to 5 parallel `/goal` on Claude Code + Codex for the heavy 80 percent; Mon calls + quick wins; Tue last 20 percent; Wed soak; Thu launch. Quality is a practitioner eval (Carly score 27.9 -> 51.3); she cannot edit her own emails (anti-overfit). Discovery: one news item -> several angles, chat the plan, then one research subagent per angle in its own container. `AGENTS.md`: CLI is deterministic JSON; judgment lives in skills.

### Jason Kneen

[X](https://x.com/jasonkneen) · [GitHub](https://github.com/jasonkneen)

**lazar** (2026-07/08): one tool `bash`, sandboxed; kernel source is chmod a-w and the binary is chflags-locked. Kernel edits go through a proposal ceremony, not agent write. Plans are numbered files from an improve pass (`plans/001-….md`) plus a README status table. Each plan: drift check against a pinned commit, Why, Current state excerpts, Scope in/out, Git workflow, Steps with per-step verify, Done criteria, STOP conditions. Rejected findings listed so nobody re-audits them. Executors are worktree-isolated subagents; the operator merges.

### Jeffrey Emanuel

[X](https://x.com/doodlestein) · [GitHub](https://github.com/Dicklesworthstone)

**agent-flywheel** (2026-08-21): huge iterated plans -> beads (epics / tasks / deps) -> swarm. Two plan layers: short `PLAN_TO_*.md` (non-negotiables, source of truth, phases + acceptance, quality-gate commands) then `COMPREHENSIVE_PLAN_FOR_*.md` (numbered book 0-N) plus satellite `docs/` (ADRs, VERIFY_SPEC, negative evidence). Execution is beads, not the book. Clean-room replan (ignore current impl) then reimplement. Reality-check-for-projects bead + anti-ceremony skill. Agent mail is the coordination substrate.

### Josh Pigford

[X](https://x.com/Shpigford) · [GitHub](https://github.com/Shpigford)

**nurb evals** (2026-08) is a live `/build` run. `/research` first (codebase, docs, web, deps, UI in parallel) because Plan mode misses recent docs. Then `docs/{name}/RESEARCH.md`, `IMPLEMENTATION.md` (phased; each phase ships something testable), `PROGRESS.md`. `/build phase N` executes. A fresh-context verifier re-runs Success independently. Adversarial pass is required (a closed-tunnel clip scored 1.0; cheat kept as a failing fixture). After code: `/but-for-real`. Before commit: `/learnings` (high bar; "nothing worth adding" is valid).

### Kun Chen

[X](https://x.com/kunchenguid) · [GitHub](https://github.com/kunchenguid)

**firstmate** + **Grok Ship** (2026-08-20). `/vision` mines merged PRs, drafts a 40 to 70 line `VISION.md` (accept/refuse policy: "A change aligns when / should be resisted when"), then stress-tests on a lavish-axi board of 8 to 12 non-obvious hypotheticals. Operating model: captain talks only to Firstmate. Firstmate writes a sqlite task row (`scout` | `ship` | `decision`) and delegates. Scout = report, never a PR. Ship = Cursor cloud agent + fresh-context adversarial review; no merge without the captain's word. Chat is not the backlog.

### Lauren

[X](https://x.com/poteto) · [GitHub](https://github.com/poteto)

**pstack** `/poteto-mode` (2026-08). Does not default to planning: "the best spec is code." Playbook: `/how` the subsystem -> `/architect` (or `architect skipped: <reason>`) -> named data shape -> delegate impl to a subagent with file paths and success criteria -> verify on the real surface (compile is not done) -> small stacked commits. Throughput checkpoint as four todos (blocking first steps, independent workstreams, shared mutable state, smallest safe split). Parallel only after one agent is trusted. 2026-08: Grok Bot / Cursor at SpaceXAI.

### Lee Robinson

[X](https://x.com/leerob) · [GitHub](https://github.com/leerob)

**pixo** (Rust image compression): Cursor plan files are the spec. YAML front matter (`name`, `overview`, todo DAG with `id` / `dependencies` / `status`), then architecture mermaid and a file tree. Standing `AGENTS.md` lists `cargo test`, `cargo fmt && cargo clippy`, and "changing benchmarks? update BENCHMARKS.md." 2026-08: SpaceXAI, training Grok for the Bot harness. Grok Bot uses the Cursor cloud harness natively; not a model-picker product.

### Mario Zechner

[X](https://x.com/badlogicgames) · [GitHub](https://github.com/badlogic)

**Pi** (`pi-mono`). No 50-chapter plans. Spec is standing `AGENTS.md`: after code changes run `npm run check`; never full vitest unless asked; never commit unless asked. Git (multi-agent cwd): `git add <path>` only, never `git add -A`, never `git reset --hard` / `checkout .` / `clean -fd` / `stash`. Do not `gh pr checkout` unless asked. 2026-08: still landing harness fixes (finish-reason override, custom footer APIs). Works with Armin Ronacher on Pi.

### Matt Pocock

[X](https://x.com/mattpocockuk) · [GitHub](https://github.com/mattpocock)

**skills** repo, locked chain as of 2026-08-22: `/wayfinder` -> `/to-spec` -> `/to-tickets` -> `/implement-spec`. Specs are issues: Problem, Solution, long user stories, implementation/testing decisions, out of scope. **No file paths.** Tickets are vertical slices with blockers, one context window each. Foggy work is a wayfinder map of decision tickets, not a 50-chapter plan. `/implement-spec` (2026-08-21): research subagent, concurrent ticket worktrees, spec review, cleanup. Goal is AFK after heavy upfront alignment.

### Mitchell Hashimoto

[X](https://x.com/mitchellh) · [GitHub](https://github.com/mitchellh)

**Ghostty** Kitty Graphics (2026-08-21): he read the spec and Kitty source himself. Agents did not write the protocol. Fable + Sol ran ~3 weeks finding mismatches vs spec / Kitty / Ghostty. Four-stage test factory: Sol writes the harness; Fable+Sol ralph-loop cases onto disk; roles reverse as an adversarial judge ("Do not trust the author. Assume ill intent."); Sol dedupes. 400+ cases; pty asserts byte equality with Kitty. Ghostty `AGENTS.md`: never create an issue or PR. `AI_POLICY.md`: disclose the tool; human must understand every line; no AI media. Maintainers exempt; outside slop is denounced.

### Peter Steinberger

[X](https://x.com/steipete) · [GitHub](https://github.com/steipete)

**agent-scripts** / **camsnap** / **OpenClaw**. Do not write a plan unless the user asks. Standing policy is `VISION.md` (Merge by Default vs Needs Sign-Off). Feature work: dated design spec (Decision, Accepted behavior, Non-goals, Required tests, Recorded product choice) then a TDD implementation plan that names files and inlines failing tests. 2026-08-15: `AGENTS.md` records misses that already happened, e.g. "upload videos to each PR that changes UI state." CodexBar (2026-08-24) still shipping; changelog uses the same section names each time.

### Steve Yegge

[X](https://x.com/Steve_Yegge) · [GitHub](https://github.com/steveyegge)

**beads** (2026-06): "a knowledge graph of all your work, disguised as a lightweight issue tracker." Plan markdown is input; the live spec is the graph. `plan-to-beads`: epic, each phase a task, sequential deps, agents start at `bd ready`. Git ledger of agent steps plus forensics (why) joined to git (what / where / how). Multi-repo needs shared Dolt. 2026-06-30: personal work is "code smooshing" leftover with an agent; fleet loops do the rest.

### Thariq Shihipar

[X](https://x.com/trq212) · [GitHub](https://github.com/ThariqS)

Claude Code at Anthropic. **html-effectiveness**: specs, plans, reviews, decks, and small editors as one self-contained `.html` file (no build). Sample `16-implementation-plan.html` sections: milestones, schema and API contract, mockups, key code, risks, open questions. 2026-07: most `SKILL.md` files are too big; prefer small body, scripts inside the skill, progressive disclosure. 2026-08-21: `/eli5` skill -> HTML artifact, big pictures, few words.

### Thibault Sottiaux

[X](https://x.com/thsottiaux) · [GitHub](https://github.com/thsottiaux)

Leads Codex at OpenAI. Dev Interrupted (2026-01): "Scaffolding is coping not scaling." The harness is meant to be removed as the model gets better, or you get capability overhang (the wrapper limits the model). Build the agent first; discover scalable primitives; let the model do the work. 2026-08: 20M Codex actives; public ops on rate limits, image+compaction waste, conversation-title drain. Cache hit rate is how long sessions stay cheap. Supported surface: Sign in with ChatGPT on official clients or OSS (Pi, OpenCode).

### Trevin Chow

[X](https://x.com/trevin) · [GitHub](https://github.com/tmchow)

**compound-engineering-plugin**. 2026-08-24: `/ce-strategy` writes `STRATEGY.md` (VISION.md equivalent); every later CE skill reads it. 5 to 10 minutes of human thought, then the file steers. Chain: `/ce-ideate` -> `/ce-brainstorm` -> `/ce-plan` -> `/ce-work`. ce-plan is rails not choreography: decisions, in/out of scope, atomic U-IDs (never renumber), files each unit touches, test scenarios, risks. No exact signatures or shell steps. 2026-08-18: Fable does brainstorm+plan; `ce-handoff` to Codex Sol as orchestrator, Luna High subagents on ce-work. Skills cut ~70 percent smaller in v3.23 (load essentials, pull procedures on demand).

### Trevor I. Lasn

[X](https://x.com/trevorlasn) · [GitHub](https://github.com/trevorlasn)

**0xinsider** (2026). The spec of the product is the API: REST, local MCP (`@0xinsider/mcp`), remote MCP, `llms-full.txt`, unauthenticated discovery of the full authenticated route index. Recipes (insider-scanner, copy-trade, alert-bot) are the procedures. 2026-06: "every ticket is just a spec for the next fix." Repeated workflows become skill files the agent reads; pin skills to package version so the agent cannot wire a stale pattern. 2026-05: copy-on-write on 0xinsider for months (branch per task, test destructive work, throw the branch away).

## License

This repo's own words are for learning and reuse in your agent setup. Samples from other folks stay under their own licenses. Follow the source links.
