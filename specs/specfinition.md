# Specfinition

A spec is the destination document. It says what must be true when the work is done. It does not say how to type it, and it does not name files.

Skip writing a spec when there is no real decision — a rename, a one-line fix, a tool that is already obvious. Write a spec when the outcome, bounds, or proof would otherwise be guessed.

Write in **positive directional language**: every sentence names the destination or a step toward it. Lead with the verb of the correct action. State the correct path so the wrong path has no room. Reserve NEVER/MUST for true invariants (safety, money, deletes, secrets).

**No file paths, no function names, no code snippets.** Those rot. Durable names stay: routes, schema fields, command names, domain terms, U-IDs. Exception: a tiny snippet that *is* the decision (a state machine, a schema, a DSL production) — the decision-rich part only.

**The whole spec uses the domain language.** Once terms are agreed, every section — problem, success, call contract, architecture, current system — speaks those terms and only those. Do not drift to synonyms. A spec is not complete until domain language is agreed with the user.

Units of work in the spec are **behaviors**, tagged with **stable U-IDs** (`U1`, `U2`, …). Never renumber. Split keeps the original id on the original concept; new work takes the next unused number; deletes leave gaps. Later tickets and plans cite U-IDs, not “the third bullet.”

Per-part **description** and **instructions** live in [components.yaml](components.yaml). Instructions are restated under each heading below.

---

## Where specs live

In a project: `docs/specs/YYYY-MM-DD-<slug>.md`

- **Date** (ISO, the day the spec is agreed, or first drafted if still draft) is in the filename and in front matter. Dates order iterations. A later date does not automatically replace an earlier one — two specs can land the same week on different parts of the system.
- **Slug** comes from domain language (the main concept, kebab-case), not from a cute phrase.
- One spec, one file. Do not append a new iteration into an agreed spec. Write a new dated file and set `parent` to the spec it iterates.

**Dates sort. `parent` names the lineage.** If this spec is the next round of change on the same slice, `parent` is that earlier file. First spec in a line omits `parent`. Work on a different slice is a different file with no parent — not a second kind of link.

A brownfield upgrade of something already specced sets `parent` to that spec. If you cannot name the predecessor, current system has to reconstruct it.

Tickets, plans, and beads cite the spec by path and U-ID (`docs/specs/2026-08-24-camera-list.md#U3`). The spec stays the destination; those artifacts do not fork new names for the same concepts.

### front matter

Fill title, date, status, slug. Set parent only when this spec iterates an earlier one. Do not add extra fields.

```yaml
---
title: <domain-language name of this change>
date: YYYY-MM-DD
status: draft | agreed | superseded
slug: <kebab from domain language>
parent:           # relative path to the spec this iterates, or omit
---
```

`status: agreed` only after domain language is settled with the user. `superseded` when a newer spec sets `parent` to this file. Leave the old file in place; do not rewrite history.

---

## Sections

Use these headings. A blank **edit whitelist**, **edit blacklist**, **automation metric**, or **automation budget** means that part is not used. Do not invent a constraint from an empty list.

### problem

Always include. Name who hurts and what they cannot do today. Stay in the user's world, not the code. If several pains exist, mark which this spec addresses.

The pain from the user's side. What is broken, missing, slow, unsafe, or confusing **today**. Write it so someone who has never seen the repo still feels the gap.

“I cannot tell which camera failed” is a problem. “The error type is too wide” is not — that belongs in current system or design decisions if it is the cause.

If several pains exist, list them; mark which this spec actually addresses. The rest go to out of scope or later work.

### solution

Always include. Same altitude as problem. One or two paragraphs of the new outcome. Do not preview architecture, data models, or work units here.

What becomes true for that user when this spec is done. Outcomes, not modules. A reader should be able to accept or reject the solution without knowing how it is split.

If the solution is a constraint (stop doing X) rather than a new verb, say that plainly.

### user stories

Write enough to cover edges. Tag a story with a work-unit id when this spec delivers it. Untagged is context, not work.

A numbered list, long enough to cover the feature. Short lists hide edges (empty state, auth failure, second camera, replay after crash).

```
1. As a <actor>, I want <capability>, so that <benefit>
```

Actor is a role that actually exists (operator, camera, CI, another agent). Capability is a verb they can observe. Benefit is why they care — skip stories whose benefit is “so that the system is better.”

Untagged does not mean “do it anyway.” Stories that contradict out of scope or later work do not belong here. Split a story that smuggles two capabilities.

### success

Always include. Each line is a checkable fact on a real surface. Inconclusive is fail. Do not list chores.

A stranger can tell pass from fail without reading the code and without being told which test file to run.

For each line:

- Name the **surface**: CLI stdout/stderr, HTTP response, on-screen state, a file the user opened, a log line they would read, a score an eval prints.
- State the observation: what appears, what does not appear, what is allowed to fail closed.
- **Prove on the real surface.** Typecheck, compile, and mock-green are not done. Run the path a user (or the eval they would trust) actually runs.
- Tie the line to a U-ID when the mapping is not obvious.

Write success as facts (“`list` prints names and never prints passwords”), not as chores (“add tests for list”). How those facts get automated lives outside this spec.

### out of scope

Named no's for this spec. Do not put later work here.

Work a reasonable agent would otherwise pull in because it is adjacent, tempting, or “while we're here.” Each item is a capability or surface, not a vibe (“no polish”). If something is wanted later rather than never, put it under later work.

### later work

Wanted, not this spec. Do not build it. Let it shape the current design so this work does not paint that future shut.

No U-IDs here. Authorized behaviors live under work units. later work is a parking lot so the agent does not grow scope when it gets bored or clever.

### edit whitelist

If blank, it is not used. Do not read empty as "edit nothing." When present, only these domain surfaces may change. Name by domain, never by path.

“The camera config store,” “the JSON-RPC stdout contract,” “auth cookies.” Not “the config package.”

### edit blacklist

If blank, it is not used. Do not read empty as "edit everything" or "edit nothing." When present, those domain surfaces are read-only for this spec even if a better fix lives there.

Cannot-edit is an invariant of *this change*, not of the whole program (program-wide rules go under invariants).

### invariants

Keep the list short. A goal can complete; an invariant can only be upheld. Reserve NEVER/MUST for these lines.

True before, during, and after this spec. Protocol, safety, cancel, secrecy, “stdout is JSON-RPC only,” “passwords never appear in list output.” They survive later work.

If everything is an invariant, nothing is — demote the rest to success or design decisions.

### design decisions

Record a row only when a reader would ask why this, not the other thing. Skip anything already obvious from problem or solution.

| ID | Decision | Why this, not the obvious alternative |
|----|----------|----------------------------------------|
| D1 | … | … |

Good row: “list never prints secrets because operators paste CLI output into tickets and logs.” Bad row: “use JSON because we already use JSON.”

Do not use this table as a changelog of the design session. Unique or contested calls only.

### open questions

Write the options already visible. If the work cannot ship without an answer, it is not open.

Questions this spec does not settle. A later spec, a prototype, or a human call. Unresolved on purpose, not forgotten. Close it in design decisions or cut the work unit that depends on it.

### call contract

Show named verbs a caller runs and what must never appear in output. If there is no user-facing surface, say so and point success at the remaining observable.

The verbs a user or caller actually runs: commands, routes, RPC methods, flags, event names. Show example invocations that a human could paste. State required vs optional inputs. Durable names only (the command `snap`, the route `/v1/cameras`, the field `name`). No handlers, no routers-as-files.

This is the contract at the edge, not an implementation sketch, and not shell the implementer runs.

### data models

Show YAML or JSON of the data, not of source files. Name entities in domain language. Show one happy record and the empty cases success cares about.

The durable shapes: config, records, events, schema fields, identity, what is required vs optional, what is secret vs listable. If two representations exist (on disk vs on the wire), show both and which is canonical. Do not invent tables, ORMs, or serializers here. Shape and meaning only.

### architecture

Map modules, interfaces, seams, edges. If no new module and no changed edge, one line naming where behaviour lands. Not a file tree.

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

When current system is shallow or sticky, `/improve-codebase-architecture` is the scan for deepening opportunities (friction, leaky seams, tests that cannot sit at the interface). This spec does not run that whole report; it **uses the same words** when proposing modules so a later deepening pass does not have to translate.

Write:

- **Modules** — domain-language name, one job, what it owns and must not own. Name after a concept, not a generic role (`Engine`, `Manager`, `Helper`).
- **Interface of each new or changed module** — the facts a caller must know, in short. Hide the rest.
- **Seams** — where those interfaces sit; what is allowed to vary behind them.
- **Edges** — who may call whom, direction, sync vs async, what never crosses (secrets, stdout vs stderr).
- **Placement of each U-ID** — which module is on the hook, without naming files.

current system is *as-is*; architecture is *as-required by this spec*. Call out the delta here.

### domain language

Infer product terms already in use; do not invent stand-ins. Agree with the user before status: agreed. After that, no synonym drift. Always include.

This is one of the most important sections. Crystallizing the problem space into shared words is a massive win — including names for **forces, tensions, and other factors** people can already feel but have not labeled.

**Must adhere.** After agreement, the agent uses these terms in the spec, in tickets, in plans, and in later conversation. No synonyms, no slide back into generic software words (`system`, `pipeline`, `engine`, `sync`, `manager`) when a domain term exists.

#### How to get there

Treat naming as part of writing the spec, not a glossary bolted on at the end. As problem, current system, and architecture surface a concept, **stop and name it with the user**.

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
- Modules (using the architecture names)
- States and lifecycle cuts (definition vs run, planned vs observed, source vs target)
- **Forces, tensions, factors** that drive decisions (the thing you keep arguing about — give it a name)
- The DSL if the work *is* a language: productions and meaning, designed before runtime types

Keep definitions tight. General programming terms stay out unless this project means something special by them.

Public, persisted, CLI, route, and schema names are migration-sensitive; treat them as contracts once agreed, not as drafts to keep cycling.

### current system

If blank, it is not used (greenfield). When present, snapshot what exists now. Do not write wishes here.

Brownfield and upgrades: behavior, contracts, failure modes, who calls whom, what callers already believe, invariants already in force, what stays. Depth matches blast radius. A small additive flag: a short paragraph. A store rewrite: the real topology, the failure modes people already hit, the contracts you must not silently break.

APIs that do not exist yet belong in solution, call contract, and data models.

When current system and architecture would repeat, current system is *as-is*; architecture is *as-required by this spec*. Call out the delta in architecture, not by restating the whole map twice.

### automation metric

For auto-research loops (keep vs discard a trial), not ordinary product work. If blank, it is not used. When present, one number, directional, measured the same way every run. Write with automation budget, or neither. Do not invent a vanity score.

A good metric is:

- **One number** (or a tiny ordered set) the agent may move.
- **Directional** — higher/lower/within-band, stated.
- **Measured the same way every run** — same harness, same hold-out, same clock.
- **Hard to game from inside the change** — independent of the code under edit, or a hold-out the agent must not touch.
- **Comparable across experiments** — `val_bpb` is vocab-size-invariant so architecture changes stay fair; raw wall-clock alone is not, across machines.
- **Paired with a simplicity tie-break** — a 0.001 gain that adds a pile of machinery loses to equal score from deleting code.

If you cannot name a metric that would change a decision, you do not have one. Leave it blank.

### automation budget

For auto-research loops. If blank, it is not used. When present, the cap that ends a trial (wall-clock, tokens, runs). Write with automation metric, or neither.

The metric decides keep/discard; the budget decides when a trial is over. Wall-clock per trial (e.g. always 5 minutes of train, kill at 10), token cap, max runs, max parallel. The budget makes trials comparable and stops “one more tweak.”

### risks

What might go wrong in this change. Not halt rules for the executor.

### work units

Always include. Stable ids (U1, U2, …). Never renumber. Split keeps the original id; new work takes the next unused number.

Named behaviors this spec is on the hook to deliver. Later tickets and plans cite these ids.

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

## problem
## solution
## user stories
## success
## out of scope
## later work
## edit whitelist
## edit blacklist
## invariants
## design decisions
## open questions
## call contract
## data models
## architecture
## domain language
## current system          <!-- blank = not used (greenfield) -->
## automation metric       <!-- blank = not used -->
## automation budget       <!-- blank = not used -->
## risks
## work units
```
