---
id: E0006
type: evidence
title: "The operator rejected a profile that passed every marker"
description: "A document scoring 8 of 8 on the profile's own markers was rejected by the operator as an impression of their voice; the two causes were headings and invented landing sentences, neither of which any marker measures."
timestamp: "2026-11-09"
tags: [voice, profile, verification, findings]
status: active
amends: [E0005-markers-are-genre-sensitive-and-the-checker-must.md]
---

The map handoff rewritten under the first real voice profile passed **8 of 8**
countable markers ([E0005](E0005-markers-are-genre-sensitive-and-the-checker-must.md)).
Shown it in a browser beside the original, the operator's verdict:

> "i think it sounds like you doing an impression of me. headings like ''what a
> column of addresses can't tell you'' sounds pretty weird, it's not something
> i'd write as an opening heading. I'd probably say something like 'Why we built
> a map'."

This is the single most useful measurement the project has taken, because it
settles something that was previously an argument: **a full marker pass is not
evidence that a profile works.** Every number was inside its range and the prose
was still wrong.

# Cause 1 — headings were never a measured population

The profile measured sentences, punctuation, diction, hedging and rhetorical
moves, all derived from paragraph prose. It said nothing about headings. So the
rhetorical moves found in the operator's *paragraphs* — reframing, negation
constructions like "The problem isn't that models want to lie" — were applied to
a *heading*, where the operator never uses them.

Checked against the corpus afterwards, which should have happened first.
Training-set headings take three shapes and nothing else:

| Shape | From the corpus |
|---|---|
| Noun phrase naming the subject | "Background Information", "The Optimization Loop", "The LLM-as-Judge Problem", "Bash Uploader Deprecation Plan" |
| Plain question, usually from the reader's side | "Why did Codecov build Impact Analysis?", "How do I Use the New Uploader?", "How Can Impact Analysis Help Me?" |
| "What X" naming what follows | "What We Measure (and Why Accuracy Comes First)", "What the Pipeline Actually Looks Like" |

Plus one imperative to close: "Start with Measurement".

**Not one of the corpus headings withholds its subject.** And the operator's
proposed fix, "Why we built a map", is a near-exact match for a heading already
in their corpus — "Why did Codecov build Impact Analysis?" Their instinct
matched their own writing; the generated heading matched neither. The evidence to
get this right was sitting in the training set, unexamined because headings were
not in the population being measured.

# Cause 2 — landing sentences coined instead of compressed

The profile named the operator's strongest rhythm feature correctly — a long
analytical build ending on a short declarative — and then reproduced it wrongly.

In the corpus, these landings **restate or label what the paragraph just
established**: "We test what we ship." follows a description of the deployed
agent. "Build them first." follows the whole argument. "That's a feature, not a
bug." labels a limit just described.

The rewrites instead **coined new material** at the landing position: "That last
part is the one that costs you later" (introduces a cost the paragraph never
mentioned), "If it's misbehaving in front of a client, that's the lever" (a
metaphor arriving from nowhere), "exactly as cheerfully as a current one" (a
flourish), "the half that turns this from a sending tool into a record" (a
reframe the paragraph had not earned).

Each is defensible in isolation. Together they are the impression: a flourish
appearing where the operator would have restated something plainly. **The
distinction is mechanical enough to state as a rule** — if the short sentence
contains a claim the paragraph did not make, it is not this writer's landing.

# What this says about the verification design

[D0018](../decisions/D0018-a-voice-profile-states-its-claims-checkably.md) is
not wrong, but the weight it implies is. Markers caught real things here —
contractions 0 to 21 per 1,000 words, three semicolons removed from a corpus
that contains one in 5,685 words — and all of it was invisible to the reader
compared with two failures no marker can see.

[E0004](E0004-what-the-professional-craft-skill-could-not-say.md) predicted the
ratio from the other direction, counting seven uncountable gaps against six
countable ones. This is the same finding arriving as a measurement instead of a
prediction, and it raises the priority of the held-out regeneration diff, which
is the only check in the design that could have caught either cause. **It has
still not been run.**

# Fixes applied

- The profile gained a **Headings** section derived from the corpus, stating the
  three shapes, the prohibition on withholding, the "Why we built X" form, and
  Title Case as a default that defers to the destination's house style.
- The landing rule became "compress, never coin", with the four rejected
  inventions named so the failure is recognisable.
- Both documents were corrected: headings to "Why we built a map" and "Why we
  built the packet", and every coined landing cut or made plain.
- The profile's `verified:` field now records that the operator reviewed it,
  that markers passed, and that the prose was rejected anyway.

# Citations

- Operator review, 2026-11-09, in session — both documents shown in a browser
  beside their originals
- `~/.claude/voice/profile/professional.md`, revised the same day
- [T0015](../../tasks/voice/T0015-build-the-professional-profile-from-real-samples-and.md)
