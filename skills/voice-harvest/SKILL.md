---
name: voice-harvest
description: Use when tuning a voice profile against a person's judgement — generate passages from their own content, ask what is wrong with each, and encode what they name as rules. Run it after a first profile exists and whenever generated prose still reads wrong.
---

# Harvesting defects

This is the one step of the voice workshop with evidence behind it. Two runs:
eight passages produced eleven usable rules, and a paragraph-by-paragraph review
of one document produced roughly fifteen more. No finding from either run has
been retracted.

The comparison it replaced — showing three versions and asking which is best —
produced two rules from nine trials, and two findings that had to be withdrawn.

## The one rule that makes it work

**Ask what is wrong. Never ask which is better.**

A blind preference ranking is not a weak signal, it is a **misleading** one.
Human raters prefer text with higher model probability independent of quality —
measured at α̂ = 0.57 and 0.65, p < 10⁻¹⁴ (arXiv 2510.01171, in
`REFERENCES.md`). Tuning on someone's blind preference walks their voice toward
generic model prose, and no marker will show it happening.

The reasons people give are not subject to that. "The bullets are too long" and
"that heading names two things" are specific, defensible on reflection, and each
became a rule. "This one's better" became nothing.

Rankings are a sanity check. They are never the objective.

## Before you start

You need a profile to improve, a register to work in, and **content the person
knows**. Their own published writing is ideal: they can tell when a passage is
wrong about something, which catches defects that abstract prose hides.

Tell them what it will cost. Eight passages is about twenty minutes and is
enough to produce ten or more rules.

## Running it

### 1. Build content-only briefs

A brief carries every fact, number, date, product term and argument, in order,
and **no headings and no phrasings**. Headings especially — heading style is
usually the most recognisable thing about a writer, and a brief that leaks their
headings makes the one question most worth asking untestable.

Have a **separate agent** read the source and write the brief, then verify it
mechanically:

```python
# candidate headings: 2-12 words, under 80 chars, no terminal punctuation
heads = [l for l in lines if 2 <= len(l.split()) <= 12
         and len(l) < 80 and not l.endswith(('.',':',';',','))]
leaked = [h for h in heads if h.lower() in brief.lower()]
# plus shared 8-word shingles between source and brief
```

Target zero leaked headings. The first brief written this way leaked **10 of
13** and had to be rewritten. Some phrase overlap is unavoidable where the
content is technical — file paths, yaml keys, version strings — and that is
fine. The author's own sentences are not.

### 2. Generate with a fresh writer

**Not the session holding the profile.** An agent that has read the person's
corpus cannot write a passage uncontaminated by it, and cannot judge its own
output either. Dispatch a sub-agent that has read the brief, the craft skill and
the profile, and nothing else.

Forbid it the corpus, the source documents and any earlier arm's output,
explicitly and by path.

### 3. Present the passages

Short. Eight passages of 90–120 words beats two documents — more judgements,
less reading, and each one independent.

Vary the population: headings, openings, middles, closings. Headings are where a
person's recognition is sharpest, and 30 words of heading can be worth more than
300 of prose.

**Normalise the rendering.** Strip markdown so no passage is identifiable by its
markup. A trial that left link syntax intact handicapped one arm in exactly the
comparisons it won.

Mixing in a few passages of the person's **own** writing is useful and should be
disclosed. Tell them the composition — "some of these are yours" — and not the
labels. It is not a trap: what they would change about their own writing is
legitimate data for a profile aimed at prose they would sign.

### 4. Ask, once per passage

> What's wrong with this one?

Nothing else. No ranking, no comparison, no "which sounds more like you".

**"Nothing wrong with this one" is a real answer** and should be invited. Two
clean passes out of eight told us as much as the defects did.

If they volunteer a comparison anyway, record it — but do not ask for one.

### 5. Encode what they named

A usable defect names something specific and would survive the person being
asked to defend it in writing. "The bullets run too long" qualifies. "It's a bit
off" does not — ask what about it.

Three things to get right, each learned by getting it wrong:

**Attribute correctly.** Check whether the defect came from the brief before
blaming the writer. Three defects named in one run were phrases the brief had
supplied, faithfully reproduced. A rule aimed at the writer for the brief's
redundancy is aimed at nothing. **A phrase that survives untouched through every
draft is usually the brief's.**

**Separate content from medium.** Spoken feedback carries spoken register.
Someone saying "emails, blog posts, whatever" is not telling you "whatever" is
their written habit. Take the structure and the content of a spoken rewrite;
discard its register.

**Watch for repeats across passages.** A defect named twice is a rule; named
once it may be a preference. The strongest rule from the first run — that this
writer never leaves a head noun implicit — appeared three times: twice as a
complaint and once, most usefully, as praise for a passage that got it right.

### 6. Write the rules into the profile

Append them, grouped, with the person's own words quoted where they said it
well. A rule they named once should never need naming twice.

**Check whether the rule has now been named in a second register.** If it has,
it is not a register rule — it is a fact about the person, and it moves to the
shared profile beside the register files. Five rules reached that bar across two
harvests, and one of them *settled an ambiguity* the first register had recorded
and could not resolve on its own. Finding the same rule twice costs a review
round, which is the one resource this process actually spends.

Do not promote a rule because it looks like it generalises. One register's most
striking marker — messages starting lowercase — does not generalise at all.
Two registers, named by the person, is the bar.

**Sort craft from voice as you go.** Most of what people name is not personal.
"You used a term before introducing it" is a failure of writing for a reader and
belongs in the craft skill, where every user gets it. "I write ranges as 95% to
97%" is personal and belongs in the profile. Getting this wrong buries general
craft inside one person's file.

## When a rule contradicts the profile

It happens, and it is the most valuable outcome available.

Twice in two runs a person rejected prose that followed a rule their own profile
taught. Both times the rule was right and **unconstrained** — it needed a
condition it never had. A short declarative lands a paragraph; it does not open
one. A balanced antithesis earns its place by correcting a misconception, not by
being symmetrical.

So when someone rejects something the profile asked for, do not assume the rule
is wrong. Ask what separates this instance from the ones they like. The answer
is usually the missing condition.

## What this cannot do

It cannot tell you whether a profile makes prose sound like its owner. People
identify their own writing at about chance in blind comparison, and in one run
ranked their own published prose last in four of six trials. The best published
metric correlates with an author's own judgement at r = 0.244.

This finds **specific, nameable defects**. That is a smaller claim than it
sounds like and it is the one that has held up.
