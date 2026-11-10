# Working with this brain

The project's reasoning lives here as linked markdown with YAML frontmatter —
a graph of typed nodes, no database and no service. The files are the ground
truth, which is what makes them equally legible to a person, a diff and you.

**One principle underneath everything**
([the principle that claims must be checkable](example/knowledge-catalog/decisions/D0001-claims-must-be-checkable.md)): the
record is only worth keeping if its claims are checkable. An absent note costs
a reader nothing — they go and look. A confident, stale note costs them the
thing they would have found by looking.

## The shape

Four categories, left to right. Implementation runs forward; review runs back
and amends what it finds false.

| Category | Types | Goes in |
|---|---|---|
| **Intent** | `goal` `decision` `principle` | `knowledge-catalog/goals/`, `knowledge-catalog/decisions/` |
| **Approach** | `plan` `spec` | `plans/`, `knowledge-catalog/specs/` |
| **Action** | `task` | `tasks/<initiative>/` |
| **Evidence** | `evidence` | `knowledge-catalog/reference/`, `brief/` |

Plus `glossary` — definitional, outside the four.

**Nothing cites a node newer than itself.** A goal written today may cite
evidence from last quarter; editing that older node to point back at the new
goal is rewriting history. `superseded_by` and `amends` are the sanctioned
exceptions, because a reader who reaches a stale node must be carried to its
replacement.

**Ids** are a type letter plus four digits, flat and global: `G` goal, `D`
decision *and* principle, `P` plan, `S` spec, `T` task, `E` evidence. Always
allocate with `bin/new`; never pick a number by hand.

## Reflexes — these fire without being asked

- **Before any significant change**: `bin/relevant "<the change>"` **and**
  `bin/constraints <paths>`. The first searches by term and misses what the
  record words differently; the second lists decisions that declared they
  govern those paths.
- **Before writing code for a task**: `bin/ancestry <id> --claims`. If it says
  `⚠ UNTERMINATED`, the task has no recorded intent — say so before building.
  If an ancestor says `⚠ SUPERSEDED`, build against the replacement.
- **A contradicted decision is stated, never silently overridden.** Two exits
  only: amend it, or proceed against it with the id in the task's `# Log`.
- **Supersede, don't delete.** A decision quietly edited to match what got
  built teaches the reader that the record is written afterwards.
- **When you learn something the record doesn't know**, write it down then.
  `bin/note "<what happened>"` takes it with no type, no folder and no id —
  use it by default. Deciding what kind of thing it is costs more than writing
  it, so do that later, with `bin/which`, or never: an entry that stays a
  journal line still did its job. Reach for `bin/new <type>` when you already
  know the answer.

## Tools

| | |
|---|---|
| `bin/lint` | the gate: taxonomy, ids, links, direction, frontmatter hazards |
| `bin/doctor` | is the install sound |
| `bin/status [initiative]` | task table and the claimable frontier |
| `bin/relevant "<change>"` | what the record already says about a proposal |
| `bin/constraints <paths>` | which decisions govern these files |
| `bin/ancestry <id> [--claims]` | walk back to the intent that asked for it |
| `bin/ancestry <id> --forward` | walk on to what that intent asked for |
| `bin/reconcile [initiative]` | task status against the repository |
| `bin/note "<what happened>"` | record it now; decide what it is later |
| `bin/which` | what kind of node is this — the procedure, in two questions |
| `bin/new <type> "<title>"` | allocate an id and scaffold the node |
| `bin/stale` | countable claims that no longer match the files |
| `bin/prove <cmd>` | does that tool's output match what it did to the files |
| `bin/unread` | frontmatter the record carries that no tool reads |
| `bin/index` | rebuild folder indexes (`bin/new` calls it) |
| `bin/graph-build` | rebuild `graph.html` |
| `bin/handoff <init> --for <who>` | a self-contained page for someone outside the brain |

When an initiative holds more than one plan, mark the initiative's own with
`initiative_plan: true` — `bin/handoff` otherwise has to guess which one a
handoff is about, and it says so when it does. `--plan <path>` overrides.

## Skills, by where they sit on the picture

**Forward** — `/grill-change` → `/to-spec` → `/to-tasks` → `/implement`
**Back** — `/spec-review` (owns `Testing → Complete`), `/audit`
**Off the rails** — `/interrogate` (ask the brain anything), `/triage`,
`/wayfinder`, `/research`, `/domain-modeling`, `/code-review` (the artifact,
not the graph)

## Don't

- Hand-edit an index or a log where a skill would write it.
- Renumber anything. Ids are cited from journals, logs and commit messages.
  `bin/renumber` exists only to resolve a collision.
- Write into the host repository's own `CLAUDE.md`, `CONTEXT.md` or
  `docs/adr/`. Those are the team's: read and respect them.
- Put code in the brain, or a restatement of the code. This holds the *why*
  that points at the code.
- Fill a gap with something decision-shaped. "We didn't decide that" is an
  answer.

Depth lives in [knowledge-catalog/howto.md](knowledge-catalog/howto.md) and
[knowledge-catalog/reference/agent-skills/](knowledge-catalog/reference/agent-skills/index.md).
