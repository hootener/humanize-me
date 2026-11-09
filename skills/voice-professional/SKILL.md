---
name: voice-professional
description: Use when writing prose a person will read that stakes your judgment and owes them your reasoning — a decision memo, a status update, a code review comment, a PR description, a reply to a colleague, a recommendation. Not for text another agent will consume.
---

# Professional register

## What a claim here rests on

**The writer's judgment, stated as judgment and owned.**

That is the whole definition, and everything below follows from it. Casual
register lets a claim rest on your say-so. Research register requires evidence
outside you, cited. This register sits between them: the reader is not owed a
citation, but they *are* owed your reasoning and a name attached to it.

A professional claim therefore has two parts that agent prose routinely drops —
a holder ("I think", "my read is") and a confidence you could be wrong about.
A judgment nobody holds, at a confidence nobody could falsify, is not a
professional claim. It is a summary wearing one's clothes.

## Picking this register

Ask what the claims in this piece have to rest on. Do **not** ask what
application it is going into.

Medium and register are independent. A Slack message arguing for a schema
change is casual in medium and professional in warrant, because your colleague
is owed why and not just what. A long formal email that only confirms a time is
professional in medium and casual in warrant — there is no judgment in it to
own.

| | |
|---|---|
| This register | The reader will act on your judgment and needs to be able to weigh it |
| `voice-casual` | Your say-so is enough; no reasoning is owed |
| `voice-research` | Your judgment is not enough; the claim needs evidence outside you |

Mixed pieces are normal. Write the section at the warrant its claims require.

## Load the voice profile

Look for a professional profile, in this order, and stop at the first hit:

1. `./voice/profile/professional.md` — in the project: a team's house voice
2. `~/.claude/voice/profile/professional.md` — the writer's own

A miss is expected and is not an error. Say which mode you are in, once, before
you write:

- found → `voice: professional, profile <path>`
- neither → `voice: professional, generic (no profile found)`

With a profile, follow it over anything below that is a matter of taste. Where
it conflicts with the warrant rules above, the warrant rules win — a profile
describes how someone sounds, not what a claim is allowed to rest on.

Generic mode is a real mode, not a degraded one. Everything below applies.

## Stop doing these

These are the failures specific to this register. They are all one failure
underneath: **confidence that floats free of warrant.**

**Hedging what you should own.** "It may be worth considering whether the
migration should be split." You have a view. Say it: "I'd split the migration."
The hedge reads as humility and functions as liability avoidance, and a reader
who needs to act cannot act on it.

**Asserting what you should qualify.** The uncertain claim arrives in the same
flat declarative as the certain one, so the reader gets no gradient and has to
guess which parts you would defend.

**Judgments with no holder.** "It was determined that", "there are concerns
about", "best practice suggests". Every judgment in this register needs an
owner. If it is yours, say so. If it is someone else's, name them. If nobody
holds it, cut it.

**Never not knowing.** "I don't know" and "I'd want to check X before
committing to that" are normal professional moves and almost absent from agent
prose. Refusing to say it makes everything else you say worth less, because the
reader learns your confidence carries no information.

**Calibration that doesn't calibrate.** "Potentially", "in some cases",
"often", "this could be an issue" — unfalsifiable, so they cost nothing to say
and tell the reader nothing. Calibrate like a bet instead: "probably", "I'd be
surprised if", "I've hit this twice", "maybe one in five".

**Stacked hedges.** "This might possibly be somewhat slower." Each qualifier is
defensible alone; together they cancel the sentence.

**Symmetric both-sidesing.** Pros and cons at equal length, no weighing. In
this register you are being paid for the weighing. List the considerations if
they help, then say which way you come down and why.

**Framing before saying.** "I wanted to reach out regarding the deployment."
"There are a few things to consider here." The first sentence announces that a
sentence is coming. Open on the claim.

**Closing by summarizing.** A recap of what the reader just read, in place of a
consequence, an ask, or a decision. If there is nothing to ask for, stop at the
last real sentence.

**Bullets over continuous reasoning.** Bullets are for enumerable parallel
items. An argument runs on connective tissue — *because*, *which means*, *the
catch is* — and bulleting it keeps the conclusions while deleting the reasoning
that made them worth anything. If the items would each need a "therefore", it
is a paragraph.

**Warmth standing in for a view.** "Great question." "This is a really
interesting problem." Warmth is fine where it is sincere; warmth placed exactly
where a judgment was requested is evasion, and the reader can tell.

**Over-qualifying the obvious, under-qualifying the speculative.** The risk
weighting inverted. Hedge in proportion to how likely you are to be wrong.

## Do these instead

- **Lead with the conclusion, then earn it.** The reader may stop after the
  first line; make that line the one worth having.
- **Name the strongest objection yourself.** State it plainly and answer it.
  Volunteering the best counter-argument is the clearest signal that you
  actually weighed it, and it costs nothing you were going to keep.
- **Own every judgment.** "I think", "my read is", "I'd bet", "I'd push back
  on that".
- **Make confidence falsifiable.** Say what would change your mind, or what you
  would need to see.
- **Prefer the concrete.** A number, a case, a specific failure. "This gets
  slow" is weaker than "this is about four seconds on the staging dataset".
- **End on the consequence or the ask.** What happens next, or what you need
  from the reader.
- **Disagree in the declarative.** A disagreement softened into a question
  ("have we considered whether...?") makes the reader do the work of finding
  your actual objection.

## Before you send it

Three questions, in order:

1. **Is every judgment owned, and is every confidence something I could be
   wrong about?** An unfalsifiable hedge is the signature failure here.
2. **Did I weigh it, or did I only list it?** If the reader still has to decide
   which consideration matters, I have not done the job of this register.
3. **Would the first sentence be worth reading on its own?**

Then read it once more and cut the framing sentences. There are usually two.
