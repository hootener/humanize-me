---
id: D0021
type: decision
title: "A profile is derived per text population, not from paragraphs alone"
description: "Headings, captions, list items and paragraphs are measured and described separately, because a move that is characteristic in one is wrong in another."
timestamp: "2026-11-09"
tags: [voice, profile, method]
status: active
serves: ../goals/G0003-an-agent-writes-human-facing-prose-in-the.md
invariant: "Every text population a profile's register will produce is measured from the corpus separately, and a profile states which populations it covers."
constrains: [voice/profile, skills]
---

# Context

The first real profile was built from paragraph prose: sentence rhythm,
punctuation rates, diction, hedging, rhetorical moves. Headings, captions and
list items were filtered out of the measurement as noise — correctly, for the
markers being computed, since a figure caption is not a sentence.

Nothing then put them back. The profile described the operator's paragraph
moves and said nothing about any other population, so when a document needed a
heading, the paragraph moves were the only guidance available and they were
applied there.

The result was rejected by the operator as an impression of their voice while
passing 8 of 8 markers
([E0006](../reference/E0006-the-operator-rejected-a-profile-that-passed-every.md)).
The corpus had the answer — the operator's headings take three plain shapes and
never withhold their subject — and it went unread because headings were not in
the population being measured.

# Decision

A profile is derived per text population. At minimum: **paragraphs, headings,
list items, captions.**

Each population is measured from the corpus on its own, and a profile states
which populations it covers. A population the corpus cannot speak to is named as
uncovered rather than left to be filled in by the nearest available guidance.

A rhetorical move is recorded **against the population it was observed in**. A
move characteristic of this writer's paragraphs is not thereby licensed in their
headings, and a profile that does not say where a move belongs will have it
applied everywhere.

# Alternatives

- **Derive from paragraph prose and let the craft skill handle the rest** —
  what happened by default, and it failed. The craft skill cannot hold the
  answer, because heading style is personal: it is exactly the kind of fact
  [D0013](D0013-the-craft-ships-generic-and-the-voice-is.md) forbids a shipped
  skill from carrying.
- **One undifferentiated measurement over all text** — rejected on the
  measurement evidence: counting captions and UI labels as sentences moved the
  median two full words and produced a spurious failure
  ([E0005](../reference/E0005-markers-are-genre-sensitive-and-the-checker-must.md)).
  Separating the populations is what makes either measurement meaningful.
- **Headings as a one-off addition, no general rule** — rejected: the same gap
  exists for captions and list items, and the casual and research registers
  would each hit it again. One correction per population per register is three
  times the cost of a rule.

# Consequences

- The profile format needs a population dimension, alongside the text
  population and genre scope that
  [E0005](../reference/E0005-markers-are-genre-sensitive-and-the-checker-must.md)
  already asked for. All three land on the format spec.
- Corpus extraction has to preserve structure rather than flatten to text.
  The first build flattened HTML to plain text early, which is why headings were
  unavailable without going back to the sources.
- A profile that covers only paragraphs is **incomplete, not merely thin**, and
  should say so where a reader will see it.
- The casual and research profiles inherit this before they are built, which is
  the whole reason it is a decision and not a note on one profile.
