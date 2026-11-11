---
name: voice-precise
description: Use when writing something a person will read where your judgment is not enough and the claim needs evidence — an incident post-mortem, a measurement write-up, an analysis, a report whose numbers someone will act on. Not for text another agent will consume.
---

# Precise voice

## What a claim here rests on

**Evidence outside the writer, and the prose is exact about what that evidence
does and does not support.**

Both halves matter. The casual voice rests on your say-so and the professional
voice on your judgment, stated as judgment. This one rests on something a reader
could go and check. And a confident sentence resting on good evidence but vague
about its bounds fails here just as surely as an unsupported one.

**This is not a voice about academic subjects.** An incident post-mortem, a
pricing analysis, a benchmark write-up and a capacity estimate all belong here.
A speculative paper does not.

## Picking this voice

| | |
|---|---|
| `voice-casual` | your word is enough |
| `voice-professional` | the reader needs your reasoning |
| this voice | the reader needs the evidence, and its limits |

Pick it by what the claims require, never by the document type. A two-line Slack
message reporting a measurement someone will act on belongs here. A long report
full of opinion does not.

## Load the shared craft and your profile

**Read `../_craft/writing-for-humans.md` first.** It holds what agent prose gets
wrong in every voice — reader-modelling, correctness, rationed effects, the
sentences and vocabulary that give a machine away. Most of the work is there.

Then look for a profile for this voice, in order, and stop at the first hit:

1. `./voice/profile/precise.md` — in the project: a team's shared voice
2. `~/.claude/voice/profile/precise.md` — the writer's own

If either exists, also load `common.md` from the same directory and apply it
alongside. Where a profile and `common.md` disagree, the profile wins.

**A miss is expected and is not an error.** Say which mode you are in, once:

- found → `voice: precise, profile <path>`
- neither → `voice: precise, generic craft (no profile found)`

## Every claim carries its warrant

**A number arrives with what produced it.** Not "latency improved by 40%" but
"p99 latency fell from 820ms to 490ms across the 2.1M requests in the week after
the change." Denominator, interval, and what was measured.

**State the bounds in the same breath as the finding.** What the evidence covers
and what it does not. A reader who has to work out the limits themselves will
either overreach or distrust the whole thing.

**Distinguish measured, inferred and assumed**, explicitly, every time. These
are three different kinds of claim and prose that blurs them is the characteristic
failure of this voice.

**Name the source where one exists**, in words. Identifiers go to a references
section — see the shared craft.

**Say what would change the conclusion.** A finding with no stated way to be
wrong is an assertion wearing evidence's clothes.

## Precision is not hedging

The two get confused and they are opposites.

Hedging makes a claim harder to check: *"this may potentially lead to somewhat
improved performance in some cases."* Precision makes it easier: *"throughput
rose 12% on the write path and was unchanged on reads; we did not test mixed
workloads."*

**So: no vague quantifiers.** *Several, many, significantly, substantially,
dramatically, a number of* — replace each with the figure, or with an honest
statement that it was not measured.

**And no false precision.** A number reported to three decimal places from a
sample of nine is its own kind of lie.

## What this voice does not do

- **No rhetorical questions.** They belong to the professional voice.
- **Humour: `never`.** Not because the subject is solemn, but because a joke in
  a passage about evidence makes a reader wonder what else was decided for
  effect.
- **No conclusions in the summary that the body does not support.** The most
  common way a precise document goes wrong is a confident abstract over a
  careful middle.
- **No burying the limitation.** It goes with the finding, not in a section at
  the end that a reader may not reach.

## Before you send it

1. **Does every number carry its denominator and its interval?**
2. **Is every claim marked as measured, inferred or assumed?**
3. **Are the limits stated with the finding**, not after it?
4. **Have I said what would change my mind?**
5. **Would a reader who checked my sources find what I said they would?**
