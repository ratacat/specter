# Specfinition

A spec is the destination document. It says what must be true when the work is done. It does not say how to type it, and it does not name files.

Skip writing a spec when there is no real decision — a rename, a one-line fix, a tool that is already obvious. Write a spec when the outcome, bounds, or proof would otherwise be guessed.

Write in **positive directional language**: every sentence names the destination or a step toward it. Lead with the verb of the correct action. State the correct path so the wrong path has no room. Reserve NEVER/MUST for true invariants (safety, money, deletes, secrets).

**No file paths, no function names, no code snippets.** Those rot. Durable names stay: routes, schema fields, command names, domain terms, U-IDs. Exception: a tiny snippet that *is* the decision (a state machine, a schema, a DSL production) — the decision-rich part only.

**The whole spec uses the Domain language.** Once terms are agreed, every section — Problem, Success, Command surface, Architecture, Current system — speaks those terms and only those. Do not drift to synonyms. A spec is not complete until Domain language is agreed with the user.

Units of work in the spec are **behaviors**, tagged with **stable U-IDs** (`U1`, `U2`, …). Never renumber. Split keeps the original id on the original concept; new work takes the next unused number; deletes leave gaps. Later tickets and plans cite U-IDs, not “the third bullet.”

---

## Where specs live

In a project: `docs/specs/YYYY-MM-DD-<slug>.md`

- **Date** (ISO, the day the spec is agreed, or first drafted if still draft) is in the filename and in front matter. Dates order iterations. A later date does not automatically replace an earlier one — two specs can land the same week on different parts of the system.
- **Slug** comes from Domain language (the main concept, kebab-case), not from a cute phrase.
- One spec, one file. Do not append a new iteration into an agreed spec. Write a new dated file and set `parent` to the spec it iterates.

**Dates sort. `parent` names the lineage.** If this spec is the next round of change on the same slice, `parent` is that earlier file. First spec in a line omits `parent`. Work on a different slice is a different file with no parent — not a second kind of link.

A brownfield upgrade of something already specced sets `parent` to that spec. If you cannot name the predecessor, Current system has to reconstruct it.

Tickets, plans, and beads cite the spec by path and U-ID (`docs/specs/2026-08-24-camera-list.md#U3`). The spec stays the destination; those artifacts do not fork new names for the same concepts.

### Front matter

```yaml
---
title: <Domain-language name of this change>
date: YYYY-MM-DD
status: draft | agreed | superseded
slug: <kebab from domain language>
parent:           # relative path to the spec this iterates, or omit
---
```

`status: agreed` only after Domain language is settled with the user. `superseded` when a newer spec sets `parent` to this file. Leave the old file in place; do not rewrite history.

---

## Sections

Use these headings. Omit a section only when it cannot apply (greenfield has no current system; a one-shot tool may have no optimization metric).

### Problem

The pain from the user's side. What is broken, missing, slow, unsafe, or confusing **today**. Write it so someone who has never seen the repo still feels the gap.

Name who hurts (operator, end user, another agent, a downstream system) and what they cannot do. Stay in the world, not in the code. “I cannot tell which camera failed” is a problem. “The error type is too wide” is not — that belongs in Current system or Decisions if it is the cause.

If several pains exist, list them; mark which this spec actually addresses. The rest go to Out of scope or Next.

### Solution

What becomes true for that user when this spec is done. Same altitude as Problem: outcomes, not modules.

State the new capability in one or two paragraphs, then stop. Do not preview the architecture, the data model, or the U-ID list here — those have their own sections. A reader should be able to accept or reject the Solution without knowing how it is split.

If the solution is a constraint (stop doing X) rather than a new verb, say that plainly.

### User stories

A numbered list, long enough to cover the feature. Short lists hide edges (empty state, auth failure, second camera, replay after crash).

```
1. As a <actor>, I want <capability>, so that <benefit>
```

Actor is a role that actually exists (operator, camera, CI, another agent). Capability is a verb they can observe. Benefit is why they care — skip stories whose benefit is “so that the system is better.”

Tag a story with a **U-ID** when this spec is on the hook to deliver it. Untagged stories are context (how people work today, a neighboring flow). Untagged does not mean “do it anyway.”

Stories that contradict Out of scope or Next do not belong here. Split a story that smuggles two capabilities.

### Success (observable)

Checkable outputs. A stranger can tell pass from fail without reading the code and without being told which test file to run.

For each line:

- Name the **surface**: CLI stdout/stderr, HTTP response, on-screen state, a file the user opened, a log line they would read, a score an eval prints.
- State the observation: what appears, what does not appear, what is allowed to fail closed.
- **Prove on the real surface.** Typecheck, compile, and mock-green are not done. Inconclusive is fail. Run the path a user (or the eval they would trust) actually runs.
- Tie the line to a U-ID when the mapping is not obvious.

Write success as facts (“`list` prints names and never prints passwords”), not as chores (“add tests for list”). How those facts get automated lives outside this spec.

### Out of scope

Named no's. Work a reasonable agent would otherwise pull in because it is adjacent, tempting, or “while we're here.”

Each item is a capability or surface, not a vibe (“no polish”). If something is Next rather than never, put it under MVP vs next — Out of scope is “not this spec, and not silently later inside this spec.”

### MVP vs next

**MVP** — authorized this round. Every U-ID lives here.

**Next** — wanted, not authorized. No U-IDs. Next is not fog to explore inside MVP; it is a parking lot so the agent does not grow scope when it gets bored or clever.

If MVP is empty or identical to Next, the split has failed — cut until MVP is shippable alone.

### Can / cannot edit

What this work may change vs what it leaves alone — by **domain**, never by path. “The camera config store,” “the JSON-RPC stdout contract,” “auth cookies.” Not “the config package.”

**Can edit** is the blast radius you accept. **Cannot edit** is binding for this spec: the agent treats those surfaces as read-only even if a “better” fix lives there. Cannot-edit is an invariant of *this change*, not of the whole program (program-wide rules go under Invariants).

Greenfield: this section is often one line (“this spec creates the system; there is no existing surface to protect”). Brownfield: list both columns. A missing cannot-edit column is how rewrites leak.

### Invariants

True before, during, and after this spec. Protocol, safety, cancel, secrecy, “stdout is JSON-RPC only,” “passwords never appear in list output.” They survive MVP and Next.

Keep the list short. If everything is an invariant, nothing is — demote the rest to Success or Decisions. Reserve NEVER/MUST for these lines.

Invariants are not goals. A goal can complete. An invariant can only be upheld.

### Decisions (non-obvious only)

Table. Record a row only when a reasonable reader would ask “why this, not the other thing?” Skip anything already obvious from Problem/Solution (“we have a list command, so we used it”).

| ID | Decision | Why this, not the obvious alternative |
|----|----------|----------------------------------------|
| D1 | … | … |

Good row: “list never prints secrets because operators paste CLI output into tickets and logs.” Bad row: “use JSON because we already use JSON.”

Do not use this table as a changelog of the design session. Unique or contested calls only. Obvious follow-through stays in Solution or Success.

### Open decisions

Questions this spec **does not** settle. A later spec, a prototype, or a human call. Write them as questions with the options you can already see, so the next reader does not re-litigate from zero.

Unresolved on purpose, not forgotten. If the work cannot ship without an answer, it is not open — close it in Decisions or cut the U-ID that depends on it.

### Command / API surface

The verbs a user or caller actually runs: commands, routes, RPC methods, flags, event names. Show example invocations that a human could paste. State required vs optional inputs. State what must never appear in output (secrets, raw tokens, internal ids if they are internal).

This is the contract at the edge, not an implementation sketch. Durable names only (the command `snap`, the route `/v1/cameras`, the field `name`). No handlers, no routers-as-files.

If there is no user-facing surface (pure internal behavior), say so and point Success at the observable that still exists (a log, a side effect, a downstream API).

### Data model

The durable shapes: config, records, events, schema fields, identity, what is required vs optional, what is secret vs listable. YAML or JSON examples of the **data**, not of source files.

Name the entities in Domain language terms. Show one happy record and the empty/omitted cases Success cares about. If two representations exist (on disk vs on the wire), show both and which is canonical.

Do not invent tables, ORMs, or serializers here. Shape and meaning only.

### Architecture (modules)

Use the `/codebase-design` vocabulary exactly. Do not substitute "component," "service," "API," or "boundary."

| Term | Meaning |
|------|---------|
| **Module** | Anything with an interface and an implementation. Scale-agnostic: a function, a class, a package, or a slice across tiers. |
| **Interface** | Everything a caller must know to use it: types, invariants, ordering, error modes, config, performance. Broader than a type signature. |
| **Implementation** | What sits behind the interface. |
| **Depth** | Leverage at the interface: lots of behaviour behind a small interface. **Shallow** = interface nearly as complex as the implementation. |
| **Seam** | Where that interface lives — the place you can change behaviour without editing the callers. |
| **Adapter** | A concrete thing that satisfies an interface at a seam. |
| **Leverage** | What callers get from depth: more capability per fact they have to learn. |
| **Locality** | What maintainers get: change, bugs, and tests concentrate in one place. |

Aim for **deep modules**. Apply the **deletion test**: if deleting the module makes complexity vanish, it was a pass-through; if complexity reappears across N callers, it was earning its keep. **The interface is the test surface** — callers and tests cross the same seam. **One adapter is a hypothetical seam; two adapters make it real** — do not introduce a seam until something actually varies across it.

When Current system is shallow or sticky, `/improve-codebase-architecture` is the scan for deepening opportunities (friction, leaky seams, tests that cannot sit at the interface). This spec does not run that whole report; it **uses the same words** when proposing modules so a later deepening pass does not have to translate.

Write:

- **Modules** — domain-language name, one job, what it owns and must not own. Name after a concept, not a generic role (`Engine`, `Manager`, `Helper`).
- **Interface of each new or changed module** — the facts a caller must know, in short. Hide the rest.
- **Seams** — where those interfaces sit; what is allowed to vary behind them.
- **Edges** — who may call whom, direction, sync vs async, what never crosses (secrets, stdout vs stderr).
- **Placement of each U-ID** — which module is on the hook, without naming files.

This is a map of duties. Not a file tree, not a library graph, not a restatement of Current system. Current system is *as-is*; Architecture is *as-required by this spec*. Call out the delta here.

If the spec adds no module and changes no edge: “No new module; behaviour lands in &lt;existing module names from Domain language / Current system&gt;.”

### Domain language / DSL

This is one of the most important sections. Crystallizing the problem space into shared words is a massive win — including names for **forces, tensions, and other factors** people can already feel but have not labeled. A spec is **not complete** until this section is **agreed with the user**.

**Must adhere.** After agreement, the agent uses these terms in the spec, in tickets, in plans, and in later conversation. No synonyms, no slide back into generic software words (`system`, `pipeline`, `engine`, `sync`, `manager`) when a domain term exists.

#### How to get there

Treat naming as part of writing the spec, not a glossary bolted on at the end. As Problem, Current system, and Architecture surface a concept, **stop and name it with the user**.

- Propose a term. Say what it includes and what it is not.
- Ask the user to **push back or question any name that does not land 100%**. A few short iterations is enough, and it is worth it: people remember words they helped pick, and they will actually use them.
- Run a **name-review** (`/name-review`) over every term in this spec before calling it agreed. Boundary-first: map concepts, then names — do not start by renaming. One concept, one primary name; one primary name, one concept. Related names form a family; contrasting concepts contrast. Names stay clear out of context and stay grepable.
- Preserve names that already work. Prefer convergence over churn. Do not flatten a real distinction because two words look similar. Do not replace a domain word with a generic software word unless the domain word misleads.

Check both directions: same concept with two names; same name for two concepts. Same-name/different-concept is the higher-severity bug — agents merge the concepts.

Vague plan-words (`workflow`, `pipeline`, `engine`, `system`) usually mean the design is still mush. Crystalize or cut.

#### What to put in the section

For each term:

```
**Term**:
<one or two sentences: what it is>
_Avoid_: <synonyms this spec will not use>
```

Include:

- Entities and acts in the problem space
- Modules (using the Architecture names)
- States and lifecycle cuts (definition vs run, planned vs observed, source vs target)
- **Forces, tensions, factors** that drive decisions (the thing you keep arguing about — give it a name)
- The DSL if the work *is* a language: productions and meaning, designed before runtime types

Keep definitions tight. General programming terms stay out unless this project means something special by them.

Public, persisted, CLI, route, and schema names are migration-sensitive; treat them as contracts once agreed, not as drafts to keep cycling.

### Current system

Brownfield and upgrades only. Skip on greenfield.

How it works **today**: behavior, contracts, failure modes, who calls whom, what callers already believe, invariants already in force, what stays. Depth matches blast radius. A small additive flag: a short paragraph. A store rewrite: the real topology, the failure modes people already hit, the contracts you must not silently break.

This section is a snapshot, not a wish. Describe only what exists. APIs that do not exist yet belong in Solution, Command / API surface, and Data model.

When Current system and Architecture (modules) would repeat, Current system is *as-is*; Architecture is *as-required by this spec*. Call out the delta in Architecture, not by restating the whole map twice.

### Optimization metric (optional)

Not every project has one. A quick tool, a hip-shot change, a greenfield toy — often none. **Form the habit of looking.** If a number would make keep-vs-discard automatic, write it. If not, omit the section.

A good metric is:

- **One number** (or a tiny ordered set) the agent may move.
- **Directional** — higher/lower/within-band, stated.
- **Measured the same way every run** — same harness, same hold-out, same clock.
- **Hard to game from inside the change** — independent of the code under edit, or a hold-out the agent must not touch.
- **Comparable across experiments** — `val_bpb` is vocab-size-invariant so architecture changes stay fair; raw wall-clock alone is not, across machines.
- **Paired with a simplicity tie-break** — a 0.001 gain that adds a pile of machinery loses to equal score from deleting code.

**Budget** sits next to the metric when the agent would otherwise run forever. Wall-clock per trial (e.g. always 5 minutes of train, kill at 10), token cap, max runs, max parallel. The budget makes trials comparable and stops “one more tweak.” The metric decides keep/discard; the budget decides when a trial is over. Write both, or neither.

If you cannot name a metric that would change a decision, you do not have one. Do not invent a vanity score.

---

## Skeleton

```markdown
---
title:
date: YYYY-MM-DD
status: draft
slug:
parent:
---

# <title from domain language>

## Problem
## Solution
## User stories
## Success (observable)
## Out of scope
## MVP vs next
## Can / cannot edit
## Invariants
## Decisions (non-obvious only)
## Open decisions
## Command / API surface
## Data model
## Architecture (modules)
## Domain language
## Current system          <!-- omit on greenfield -->
## Optimization metric     <!-- omit when none -->
```
