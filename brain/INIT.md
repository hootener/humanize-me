# Filling a new brain

**Run this once, in the session that installed the brain.**

`bin/adopt` put the files in place; this puts the project in them. It is a
document rather than a skill on purpose
([why this is a document and not a skill](knowledge-catalog/decisions/D0010-init-is-a-document.md)): Claude Code
discovers skills when a session *starts*, so a skill created by `bin/adopt`
cannot be called by the session that just ran it. Three adoptions proved that
three times. Read this and follow it.

`bin/adopt` installed the brain. This fills it
([the placement and install decision](example/knowledge-catalog/decisions/D0004-placement-and-install.md)).

They are separate because they fail differently: `adopt` is mechanical and runs
once, this needs judgement and runs again whenever another repository is
adopted. If `brain/config.md` does not exist, stop and say to run `bin/adopt`
first.

**Two paths, and you must pick one before step 1.**

```bash
ls brain/knowledge-catalog/decisions/ brain/knowledge-catalog/goals/   # a brain already?
git -C <repo> log --oneline | head -1                                  # code history?
ls <repo>/docs <repo>/CONTEXT.md                                       # docs?
```

**Ask about the brain first.** Three rounds running, a test that looked only at
the repository gave a confident wrong answer: no commits and no docs said
*greenfield* to a catalog already holding four nodes. The branches are about
what is already in the brain; the repository is the second question, not the
first.

**Step 3 runs whichever branch you are on. Always.** Conversation history is
independent of code history, and the branch test below does not look at it. A
repository with no commits and no docs had **five transcripts holding two real
decisions**, and the branch told its adopter those steps were no-ops. Run
`bin/utterances` before you conclude there is nothing to import — it
costs one command and it is the one place that had anything.

**Greenfield** — no commits, no docs. Steps 2 and 4 are no-ops; step 3 is not.
Go to "Greenfield" at the end and come back for step 5. The first adopter ran all four against an empty project, got
`fatal: your current branch 'main' does not have any commits yet`, and found
the real material was in the conversation they were already having.

**In flight** — a codebase with history, decisions living in people's heads,
and docs in four places. That is the rest of this skill.

**Re-adoption** — **the catalog already holds nodes.** That is the whole
test, and it comes before the other two. Neither branch fits: there is nothing to import that is not
already here, and mining the transcripts surfaces *the previous run's own
work*, which a second adopter duly filed as fresh findings. **Which of the steps below apply:**

| Step | On a re-adoption |
|---|---|
| 1 · ask the four things | **Skip 1–3.** `config.md` already holds them. Ask question 4 only if no goal exists. |
| 2 · import existing docs | **Skip.** Anything importable is already imported; re-importing duplicates it. |
| 3 · mine the transcripts | **Run, bounded.** See below — most of what is there is the previous run's own work. |
| 4 · mine git history | Run if there are commits since the last node. |
| 5 · report | **Run.** Say what changed and what you left alone. |

Read what is already in the catalog **first**, ask the operator what has
changed since, and write only that. Bounding it by date does not work: everything a re-adoption produces is dated
today, so `--since` returns what no filter returns. **The bound is already in
the catalog** — every imported node names the session it came from in
`resource:`. Read those first, and treat any utterance from a session already
cited as covered.

## The rule that governs everything here

**Date every imported node by its origin, never by the import.** Stamping
today on a document written in July makes every decision citing it look like
it cites the future, and the direction rule will say so — twenty-eight times,
in the first real adoption. Take the date from the filename where it carries
one, and from `git log --follow --format=%ad --date=short` otherwise, which is
the reason to move files with `git mv` rather than copy them.

**Mark running records `append_only: true`** — a project log, an open-questions
list, a state snapshot. Their content runs ahead of their open date by design.

**Everything imported lands as `status: draft` with a `resource:` pointing at
where it came from.** You are reconstructing, and a reconstruction that reads
as a decided decision is worse than no brain at all
([the principle that claims must be checkable](example/knowledge-catalog/decisions/D0001-claims-must-be-checkable.md)).
`bin/lint` reports the draft count, so the operator can see exactly how much is
still guesswork.

Never promote a draft to `active` yourself. That is the operator confirming it,
and it is the whole value of the import being visible.

## Step 1 — ask the four things you cannot infer

1. ~~Which repository?~~ **Do not ask.** `bin/adopt` already wrote it to
   `brain/config.md` as `repos:`. Asking invites an answer that contradicts
   the file.
2. Where do docs already live — `docs/`, `docs/adr/`, a `CONTEXT.md`, a wiki,
   an exported Notion space? → **write it to `docs:` in `config.md`.**
3. What issue tracker is in use, and should `brain/tasks/` mirror it or replace
   it? → **this is a decision, not a preference.** It has alternatives (mirror
   / replace) and a consequence (two places to keep in step). Write it with
   `bin/new decision`, and record the choice in `config.md` as `tracker:`.
4. **What is this project trying to achieve?** One sentence. → a `goal` node.

The first adopter answered all four and had somewhere to put one of them.
Questions 2 and 3 went into the change log because nothing else fitted.

**Do not proceed without the fourth.** Without a goal there is nothing for a
lineage walk to terminate at, `/spec-review` has no intent to check against,
and every Approach node you write will fail `serves:`. If the answer is "a lot
of things", take the two that matter most this quarter and write those.

Write it: `bin/new goal "<the outcome>"`.

## Step 2 — import what already exists

In descending order of certainty, so the most trustworthy material lands first:

- **Existing ADRs** (`docs/adr/`, `docs/decisions/`) → `bin/new decision`,
  one per ADR, `status: draft`, `resource:` the original. Keep their words; do
  not improve them.
- **`CONTEXT.md`, a glossary, a data dictionary** → seed
  `brain/knowledge-catalog/glossary.md`, including the `_Avoid_` notes, which
  are usually the most valuable part and the first thing lost.
- **A README's architecture section** → an `evidence` node, not a decision. It
  describes how things are, which is Evidence; what it does not say is *why*,
  which is what a decision is for.

The host repository's own `CLAUDE.md` and `CONTEXT.md` are the team's: read
them, do not write to them.

## Step 3 — mine the transcript history

This is the step nothing else can do, and it is usually the richest.

```bash
bin/utterances            # what the operator said, across every session
bin/utterances --repeated # said more than once — the strongest signal
```

**Use the tool. Do not read the `.jsonl` yourself.**

An answer to `AskUserQuestion` is stored as a `tool_result` block inside a
user-role envelope, **not** as message text. Walk the transcript keeping
user-role entries with string content — the obvious approach — and you drop
every decision the operator made in answer to a direct question. What you find
in their place is the **assistant's paraphrase**, in assistant text.

Quote that, cite the transcript as `resource:`, and you have manufactured an
operator decision out of the previous agent's prose with provenance that looks
sound. `bin/utterances` reads both places and labels which is which.

**The signal is not "decision-shaped sentences".** Those are noise, and an
agent hunting them will manufacture a decision record out of ordinary chat.
The signal is:

- **The same correction, made more than twice.** The operator telling Claude
  the same thing in three different sessions is a decision or a principle that
  was never written down. This is the highest-value extraction available
  anywhere in this skill — it is precisely the knowledge the brain exists to
  stop re-deriving, and nothing else in the toolchain can see it.
- **Reversals** — "actually, don't do that", "we tried that and it broke".
  Those are Evidence.
- **Standing constraints** — "never touch X", "always go through Y". Candidate
  principles.

Present candidates in batches with the quoted source, and let the operator
accept or reject each. Do not write them unaccepted.

**Quote the operator, never a summary of them.** A line tagged `[typed]` or
`[answered]` by `bin/utterances` is theirs. Anything else in the transcript is
an agent talking, including an agent accurately describing what they said —
and a `resource:` pointing at a transcript that contains only the paraphrase
is a citation that cannot be checked by the person who would notice.

## Step 4 — mine the git history

- `git log --grep='revert\|hotfix\|actually'` → candidates for
  [the running record of what the brain has caught](example/knowledge-catalog/reference/E0001-brain-in-practice.md), which
  `/grill-change` reads first and which otherwise starts empty.
- `CODEOWNERS` → who owns what, for `owner:` on plans and specs later.
- Directories with the most churn → where the project's real complexity is, and
  therefore where decisions are most likely to be undocumented.

## Greenfield — when there is no history to mine

Steps 2, 3 and 4 find nothing. **The live conversation is the only source of
decisions that exists**, and it is a good one: the first greenfield adoption
produced two real decisions, both lifted from chat messages, and one arrived
sideways in the answer to a different question.

Apply step 3's signal discipline to the conversation instead of the
transcripts. You are looking for the same things:

- **A constraint stated in passing.** *"We do not care about prose that will
  be consumed by agents"* is a decision with alternatives and consequences,
  dropped into an opening message as an aside.
- **An ordering the operator has already settled.** *"The goal here is to make
  this an adoptable project, then we'll use the adoptable version to make our
  own voice setup, like any other end user would"* — a real sequencing
  decision, arriving in a reply to a clarifying question about something else.
- **A thing ruled out.** Anything the operator has said no to, and why.

Quote the operator's words back when proposing each one, the way you would
quote a transcript. They are the citation.

**Do not invent a decision to make the record look fuller.** A greenfield
brain with one goal and two real decisions is in better shape than one with
eight plausible ones.

**Nothing is a sanctioned outcome — but only after step 3.** The exit below is
scoped to *this conversation*; what it gates is scoped to *the project*. Take
it without having run `bin/utterances` and you can write a true sentence and
reach a false conclusion, with nothing feeling wrong. A conversation about
*evaluating* a tool contains no decisions about the project, and a session
that produced none, **with no older transcripts holding any either**, should
say so and stop:

> Nothing in this conversation settles anything durable about the project. No
> decisions written. The first one will arrive when you make it.

Reported by the second cold adopter, whose session contained zero project
decisions while the skill told them the live conversation was a good source.
An agent told material is there will find material. That is the manufacturing
this skill forbids two paragraphs up, and forbidding it without offering an
exit is what makes it happen.

**Same-day forward references are fine.** Everything written during init
carries today's date, so the direction rule cannot fire among these nodes —
a goal may link a decision written minutes later. Do not order your writes
around it or back-date anything to force a sequence. The rule is about
*imported* nodes, which carry origin dates.

## Step 5 — report what you did and what is still guesswork

```bash
bin/lint && bin/doctor && bin/graph-build
```

Then say plainly: how many nodes were imported, how many are `draft`, what you
could not find, and what the operator should confirm first. **The gaps are the
useful half of this report** — a brain that claims to have captured a project
it has only skimmed is the failure this whole skill is shaped to avoid.
