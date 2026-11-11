---
id: D0014
type: decision
title: "Registers are organized by burden of proof, not formality"
description: "The three registers — casual, professional, research — are distinguished by what a claim has to rest on, and a register is selected on that rather than on the medium it will be sent through."
timestamp: "2026-11-09"
tags: [voice, registers, taxonomy]
status: amended
serves: ../goals/G0003-an-agent-writes-human-facing-prose-in-the.md
invariant: "A register is defined and selected by what its claims must rest on, never by medium or formality."
constrains: [skills, voice/profile]
---

# Context

The registers arrived named for formality: casual for a Slack message,
professional for work, something research-shaped for evidence-heavy writing.
Three levels of dress.

Formality is the wrong axis to build on. It is surface — contractions,
greetings, whether a message opens with "Hey" — which makes it the easiest
thing for an agent to imitate and the least valuable thing to get right. An
agent already does polite registers passably. What it does badly is sit at one
level of confidence regardless of what it actually knows.

# Decision

Three registers, distinguished by how much warrant a claim has to carry.

| Register | A claim rests on |
|---|---|
| `casual` | the writer's say-so |
| `professional` | the writer's judgment, stated as judgment and owned |
| `research` | evidence outside the writer, cited |

A register is selected by asking what the claims in this piece have to rest on
— **not** by asking what application it will be pasted into. Medium and
register are independent: a Slack message defending an architecture decision is
casual in medium and professional in warrant, because the reader is owed the
reasoning and not just the conclusion. Formality follows from the medium and
lives as surface markers inside each register's profile.

The third register keeps the name `research`. It is what the operator reached
for, "research-level" reads immediately, and defining it by warrant rather than
by subject keeps it covering an incident post-mortem or a pricing analysis and
not only a paper.

# Alternatives

- **Organize on formality** — rejected: it is the half an agent already does
  acceptably, and building the taxonomy on it leaves the actual failure to a
  style note.
- **Two registers, collapsing casual into professional** — rejected: say-so
  and stated-judgment are different acts. Collapsing them means either the
  casual writing reads like a memo or the memos never show their reasoning.
- **Name the third `evidentiary`** — rejected: precise and stuffy.
- **Name it `rigorous`** — rejected: implies the other two are not.
- **Name it `technical`** — rejected: names a subject, not a warrant level.

# Consequences

- Each register skill has to state what its claims rest on before it states any
  style preference, and a register that cannot say this is the wrong shape.
- Calibration — how confidence and uncertainty get expressed — is a required
  section of every register's profile rather than an optional nicety.
- Selection logic asks about the claims, so a skill cannot route on file type
  or destination alone.
- Corpus filing inherits the axis, which is what
  [D0016](D0016-the-corpus-is-sorted-into-per-register-folders.md) asks the
  operator to do by hand.

# Amendment — 2026-11-11

*The axis stands. The third register's name does not, and the replacement
shifts its emphasis in a way worth stating rather than smuggling.*

**`research` is renamed `precise`**, at the operator's instruction:

> I also think we need to change the name of the research voice modality to
> "Precise" and state that it's very specifically for really precise,
> objective, fact-based communication.

**Why the original name failed.** This decision rejected `evidentiary` as
stuffy, `rigorous` as implying the other two are not, and `technical` as naming
a subject rather than a warrant level. It then chose `research` and claimed the
warrant definition would stop it reading as academic. It did not. `research`
names the kind of document people picture — a paper — and the voice is not about
a subject at all. An incident post-mortem, a pricing analysis and a measurement
write-up all belong here.

**What shifts, and it is not nothing.** The axis of this decision is *what a
claim has to rest on*. "Research" named that directly. "Precise" names the
**character of the prose** — exactness about what is known, how well, and what
is not — which is a consequence of the warrant rather than the warrant itself.

The register is therefore now defined by both, and the warrant stays primary:
**a claim rests on evidence outside the writer, and the prose is exact about
what that evidence does and does not support.** A confident sentence resting on
good evidence but vague about its bounds fails this register, which the old
definition did not clearly catch.

**The wording of the axis is separately dead.** The operator rejected *"what a
claim has to rest on"* twice while reviewing generated prose, calling it "too
claudy" — *"Nobody says that to another person."* His replacement, which is now
the form used in anything a reader sees:

> three different levels of proving it, or showing your work

The distinction this amendment turns on: **the taxonomy is right and its
original phrasing is unusable in the product.** The decision keeps its own
language for the record; the README, the skills and the profiles use his.

**What changed, and what deliberately did not.** `skills/voice-research/` is now
`skills/voice-precise/`, and the README, the craft skill and the placeholder
follow. Task logs and evidence nodes that say "research" are **left alone** —
they were accurate on the day they were written, and editing them would be
rewriting history rather than recording a change.
