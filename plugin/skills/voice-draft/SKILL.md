---
name: voice-draft
description: Use when turning a gathered corpus into a voice profile file — measuring markers, writing the rules, and recording what the corpus cannot support. Run after voice-gather and before voice-harvest.
---

# Drafting a profile

**Evidence level: low, and lower than the two skills either side of it.**
Gathering has failures behind it. Harvesting has a measured result behind it.
This step has four profiles built in three days and one finding that matters
more than the rest of this file put together.

**The draft is a hypothesis, not a product.** What makes a profile work is the
harvest — a person naming defects in generated prose. The draft's job is to give
that process something to correct without poisoning it first. Poisoning it is
easy, and section one is how.

## Markers are diagnostics. Never targets.

A marker is a number measured from the corpus. The temptation is to write it as
an instruction — *contractions at least 15 per thousand words* — so the output
can be checked against it. **Do not.** This was measured and it does active
harm.

In one trial, a pooled contraction floor of 15/1k pushed generated announcements
to 18–38/1k when the writer's real rate for that genre is 4–12. An arm given no
guidance at all landed closer to the writer than the profile did. The profile
was worse than nothing on that dimension, and it was worse *because* the marker
was phrased as something to hit.

So:

- Record every marker with its **denominator and the date it was measured**, so
  a later reader can re-check it instead of believing it.
- Put them under a comment saying what they are: `# diagnostics, not a gate and
  not a target`.
- Write **ranges observed**, not floors or minimums to satisfy.
- A marker that cannot be stated as a range of what was observed is not ready to
  be in the file.

## Derive per register. Never pool.

The same writer spanned 4.0 to 37.7 contractions per thousand words across his
own corpus — a tenfold spread that tracked genre, not person. A number pooled
across registers describes nobody and instructs everybody.

If a register's corpus is too thin to measure on its own, say so in `gaps:`.
Borrowing the other register's number is worse than having none.

## Record what you will not reproduce

Some of the most distinctive things in a corpus must not become rules. Record
them anyway, with their numbers, under a heading that says why they are there:

> ## Observed, and deliberately not reproduced

Two cases keep coming up.

**Things output must not do regardless of voice.** One casual corpus started
55% of messages lowercase and left 86% without terminal punctuation. Those are
the two most distinctive facts about it and neither is a rule, because output
always gets correct spelling, punctuation and capitalisation whatever the voice.
Measuring them was still right: they explain the corpus to the next reader.

**House style wearing the author's clothes.** Between two sources by the same
writer in the same register, one had 35 times the first person and a fifth of
the passive voice. The difference was a journal's style guide and its reviewers,
not him. **The more gatekept a source, the less of the author survives in it.**
Record the convention, name the gate, and mark it discarded.

## Split by what a sentence is doing, not by which source it came from

A corpus built from two kinds of source invites the rule *write like source A
and take only the evidence handling from source B*. That is nearly always too
coarse, and it was wrong once in exactly this way: the writer later rewrote a
generated line to be **more** impersonal than it was and called the result more
correct.

The axis is the sentence's job. Owning an error or a judgement is first person.
Stating a finding that generalises past the writer is impersonal. Both can be
drawn from the same corpus, and a source you discarded wholesale may be the
right model for one of the two.

## Do not write an absolute from one mode

Edited writing and unedited writing disagree about the same person. One profile
drawn from published posts carried three absolutes — no exclamations, a we:I
ratio, a parenthetical ceiling — and 7,612 words of the same writer's unedited
comments contradicted all three.

If the corpus is edited only, you may write tendencies and you may not write
`never`. Say which mode each rule came from when they differ.

## Draft structure from a measured population

The one part of a profile that demonstrably worked on first contact was
headings, and it worked because it was built from **the person's actual
headings, counted** — how many per thousand words, how long, what grammatical
shape, how often a question — rather than from a description of what their
headings are like.

Do the same for anything structural you can count: paragraph length, list use,
where a piece opens, how it closes. Describing a tendency produces an impression
of it. Counting a population produces the thing.

## Give every move a rate

A move written with no frequency is an instruction to use it every time, and
that alone produced three defects in one review round. Every move gets
`always`, `often`, `sparingly`, or `once per piece`, counted across a batch
rather than within one passage.

**A rate belongs to a move in a register.** The same construction can be a
signature move in one register and noise in another: two moves with several
confirmations in a professional profile were rejected outright as "too flowery"
in a precise one. When a rule is shared across registers, the rule travels and
the rate does not.

## The file

Write `<register>.md` beside any others, with frontmatter the voice skills and
the harvest both read:

```yaml
register: professional          # or `scope: all registers` for the shared file
built: 2026-11-11
built_from: 7 published pieces — 5 train (5,685 words), 2 held out (2,302 words)
sources: where they came from and when they were fetched
mode: edited, unedited, or both — and which rules came from which
load_with: common.md
verified: what has actually been checked, and what has not
gaps: what this corpus does not cover, in plain words
markers:  # diagnostics, not a gate and not a target
  sentence_words_median: [15, 22]
```

`verified:` and `gaps:` are the two fields that keep a profile honest after the
conversation that built it is gone. A fresh draft has had nothing verified. Say
that, in those words, rather than leaving the field confident and empty.

## Stop early

A first draft is finished when it has structure measured from a population,
markers recorded as diagnostics, and honest `gaps:`. It is not finished by being
longer. Most of what ends up in a mature profile comes from the harvest, in the
person's own words, and polishing the draft only produces more surface for them
to correct.

Hand off to `voice-harvest` and expect to be wrong.
