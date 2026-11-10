---
id: T0017
type: task
title: "Experiment: population-matched exemplar retrieval versus a described profile"
description: "Put five verbatim passages of the operator's own writing in the prompt, retrieved by text population rather than topic, and measure it against the described profile on the same briefs."
status: Not Ready
category: question
initiative: voice
blocked_by: [T0016]
timestamp: "2026-11-10"
tags: [voice, exemplars, experiment, research]
---

# What to build

A third arm for [T0016](T0016-run-the-held-out-regeneration-diff-against-a.md)'s
comparison: the same briefs, generated with **five verbatim passages** of the
operator's writing instead of a description of it, retrieved by **text
population** — headings to write a heading, paragraph prose to write paragraphs.

# Why this is interesting rather than merely next

[E0007](../../knowledge-catalog/reference/E0007-state-of-the-art-for-reproducing-a-specific.md)
gathered the evidence for the exemplar side and found the shape of the question
unresolved:

- Raw history beats a generated profile on every LaMP generation row, and the
  paper proposing profiles is the one reporting it, explaining that "any
  natural-language profile abstracts away exactly that idiolect".
- In the head-to-head, five samples with no instruction take the authorship
  metric (0.508) while the described profile takes the LLM judge (0.542) and the
  stylometry (0.761). The authorship difference sits inside the error bars, so
  the **ranking is not established** — what is established is that a profile has
  no advantage on the metric that asks "is this the same author".
- Five exemplars performs like ten.
- **Topic-similar selection measurably hurts**: 81.28% against 95.44% for random
  selection.

And the part worth doing for its own sake: **nobody appears to have published
the population-matched variant.** Topic matching has a measured negative result;
retrieving headings to write headings is untested. It is also exactly what
[D0021](../../knowledge-catalog/decisions/D0021-a-profile-is-derived-per-text-population-not.md)
already requires for deriving a profile, applied one step later at generation
time.

So this arm is a small original experiment rather than an application of a
known result, and it bears directly on
[D0013](../../knowledge-catalog/decisions/D0013-the-craft-ships-generic-and-the-voice-is.md),
which assumes the personal half of the library is a generated *description*. If
verbatim passages win, D0013's artifact is the wrong shape and the profile
shrinks to [E0004](../../knowledge-catalog/reference/E0004-what-the-professional-craft-skill-could-not-say.md)'s
uncountable seven — the negative space and the hedging floor, which no sample
states about itself.

# Acceptance criteria

- [ ] Five passages per generation, retrieved by text population, never by topic
- [ ] Run on the same briefs as [T0016](T0016-run-the-held-out-regeneration-diff-against-a.md)
      so the arms are comparable
- [ ] Judged blind alongside the control and profile arms
- [ ] A control for retrieval strategy: population-matched against randomly
      selected passages, since random is the condition that beat topic-matching
- [ ] The result recorded against [D0013](../../knowledge-catalog/decisions/D0013-the-craft-ships-generic-and-the-voice-is.md),
      which it may contradict

# Out of scope

- Shipping it. This is a measurement, and D0013 does not change on one run.
- Fine-tuning and activation steering, both ruled out in
  [E0007](../../knowledge-catalog/reference/E0007-state-of-the-art-for-reproducing-a-specific.md)
  on evidence and on API access respectively.

# Log

## 2026-11-10 — parked deliberately

The operator asked for [T0016](T0016-run-the-held-out-regeneration-diff-against-a.md)
first and flagged this one as interesting for research purposes. Blocked on
T0016 rather than merely unscheduled: without the control and profile arms there
is nothing to compare an exemplar arm against.

## 2026-11-10 — now has a sharp prediction to test

[T0016](T0016-run-the-held-out-regeneration-diff-against-a.md) found the
described profile's entire measurable effect sits in headings and is absent —
possibly negative — in prose
([E0009](../../knowledge-catalog/reference/E0009-the-profile-works-on-headings-and-not-on.md)).

That turns this experiment from "try exemplars and see" into a falsifiable
prediction. If a description carries what can be enumerated and exemplars carry
what cannot, then verbatim passages should beat the described profile **on
prose and not on headings** — the exact inverse of T0016's result. A run where
exemplars win on headings too, or lose on both, falsifies that account of why
the dissociation exists.

Run it on the same nine trials, as a fourth arm, so the comparison is direct.
