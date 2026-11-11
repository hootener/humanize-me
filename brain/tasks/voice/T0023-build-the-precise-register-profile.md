---
id: T0023
type: task
title: "Build the precise register profile"
description: "The third register, built from a split corpus — voice from a public incident post-mortem, evidence discipline from peer-reviewed papers, academic house style recorded and discarded."
status: In Progress
category: enhancement
initiative: voice
blocked_by: []
spec: ../../knowledge-catalog/specs/S0001-the-voice-workshop.md
timestamp: "2026-11-10"
tags: []
---

# What to build

A precise voice profile for the operator — the third register, and the one
[D0014](../../knowledge-catalog/decisions/D0014-registers-are-organized-by-burden-of-proof-not.md)
as amended renamed from `research` because the old name made people picture a
paper.

# Acceptance criteria

- [x] A corpus whose authorship is proven at the level it was actually written
- [x] A profile whose markers were measured rather than reasoned
- [x] House style separated from voice, with the evidence for the separation
- [x] A `gaps:` field stating what the corpus does not cover
- [ ] A harvest run against it

# Out of scope

- The `voice-precise` craft skill, which now exists and is generic per
  [D0027](../../knowledge-catalog/decisions/D0027-three-generic-voice-skills-ship-and-nothing-personal.md).
  This task builds the operator's personal profile, not the shipped skill.

# Log

# Log

## 2026-11-11 — built on a split corpus, because the obvious corpus was wrong

The operator offered peer-reviewed publications — 17 of them, 15 where he is
first or second author. Academic writing is the obvious precise corpus and it
turned out to be the wrong one.

**Measured, his academic prose is not his voice.** Across three papers: first
person 0–5.8 per thousand words, passive construction 11.6–12.7, contractions
1.4–5.1. His own public incident post-mortem — same register, same demand for
evidence, no reviewers — runs **first person 58.7, passive 2.3**. Thirty-five
times the first person and a fifth of the passive, same writer, same warrant.

That is [E0012](../../knowledge-catalog/reference/E0012-unedited-professional-writing-contradicts-three-absolutes-in-the.md)
at maximum strength. Peer review, co-authors and a journal style guide are the
most gatekeeping any of his writing has passed through, and what survives
describes the venue.

**So the profile is split.** Voice from the post-mortem: first person
throughout, active, naming error with the strongest accurate word — *"we
egregiously mishandled"*, *"we tricked ourselves"*. Evidence discipline from the
papers, where it is genuinely strongest: the parenthesis carries the precision
at 13–20 per thousand words, the highest rate of any register he writes in, and
quantities arrive with units and conditions. Academic convention is recorded
with its numbers and marked **observed, not reproduced**, per
[D0025](../../knowledge-catalog/decisions/D0025-output-is-always-correctly-spelled-punctuated-and-capitalised.md).

**Two gathering rules came out of this and are now in `/voice-gather`.**

*Ask which sections they wrote.* He identified about 3,000 words inside a
9,000-word paper where he is third author — a source a byline check alone would
have discarded whole. Only the author can answer that.

*Watch for house style masquerading as voice.* The more gatekept a source, the
less of the author survives in it, and the measurement above is the worked case.

**Thin, and said so.** One post-mortem is the entire voice sample. The everyday
precise writing someone would actually ask an agent for — an internal analysis,
a data memo, an RFC — is absent and recorded as unknown rather than covered.
