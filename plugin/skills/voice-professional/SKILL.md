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
| `voice-precise` | Your judgment is not enough; the claim needs evidence outside you, stated exactly |

Mixed pieces are normal. Write the section at the warrant its claims require.

## Load the shared craft and your profile

**Read `../_craft/writing-for-humans.md` first.** It holds what agent prose gets
wrong in every voice — reader-modelling, correctness, rationed effects, the
sentences and vocabulary that give a machine away. Most of the work is there.

Then look for a profile for this voice, in order, and stop at the first hit:

1. `./voice/profile/professional.md` — in the project: a team's shared voice
2. `~/.claude/voice/profile/professional.md` — the writer's own

If either exists, also load `common.md` from the same directory and apply it
alongside; it holds rules that writer follows in every voice. Where a profile
and `common.md` disagree, the profile wins.

**A miss is expected and is not an error.** Say which mode you are in, once,
before you write:

- found → `voice: professional, profile <path>`
- neither → `voice: professional, generic craft (no profile found)`

Without a profile you do the generic job, and that is a real mode rather than a
degraded one. A profile makes the prose sound like one particular person; the
craft makes it stop sounding like a machine, which is most of the value.

## Stop doing these

These are the failures specific to this register. They are all one failure
underneath: **confidence that floats free of warrant.**

**Claims nobody holds, at confidences nobody could be wrong about.** "It may
be worth considering whether the migration should be split." Nobody holds that,
nothing in it could turn out false, and a reader who has to act cannot. Say
"I'd split the migration" — or, hedged as heavily as you like, "I'd probably
split it, though I haven't looked at the foreign keys."

The failure is not the hedge. A hedge that names what you are unsure of, or
states a likelihood that could turn out wrong, is doing work — and how much of
it you do is your voice, not this skill's business. "It may be worth
considering" fails because after it no claim remains to be wrong about.

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

**Qualifiers that leave nothing behind.** "This might possibly be somewhat
slower." Not wrong for carrying three qualifiers — wrong because after them no
claim remains that could be false. "This is probably four seconds slower, maybe
one" carries just as many and still says something.

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

**Qualification that doesn't track the uncertainty.** Hedging the obvious
while stating the speculative flat. This is about tracking, not amount:
wherever your own hedging level sits, it has to rise where you are more likely
to be wrong, or it carries no information.

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

Five questions, in order. The first three are the craft; nothing about my voice
excuses them.

1. **Is everything still here, and nothing more?** Every link, number, label,
   caveat and instruction I was given — and no URL, figure or name I was not.
2. **Does every judgment have a holder?** Mine, or someone I named.
3. **Is every confidence something I could be wrong about?**
4. **Did I weigh it, or did I only list it?** If the reader still has to decide
   which consideration matters, I have not done the job of this register.
5. **Would the first sentence be worth reading on its own?**

Then read it once more and cut the framing sentences. There are usually two.
